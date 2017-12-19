#UE4 C++ Puzzle 模版学习和分析  

UE4 version: 4.17 
---


## 1. 核心C++类
 


PuzzleBlock： 用于交互的一个个小立方块，它包含了两类事件操作:鼠标从上面划过，鼠标单击事件。  
- Puzzle： 工程模块生成类，用于生成dll
- PuzzleGameMode：设置游戏运行模式，初始化游戏中的Pawn、Controller对象      

		 APuzzleGameMode::APuzzleGameMode()
		 {
			// no pawn by default
			DefaultPawnClass = APuzzlePawn::StaticClass();
			// use our own player controller class
			PlayerControllerClass = APuzzlePlayerController::StaticClass();
		 }


- PuzzlePawn：游戏的虚拟玩家，主要提供以下接口：  

		public:
			virtual void Tick(float DeltaSeconds) override;
			virtual void SetupPlayerInputComponent(UInputComponent* PlayerInputComponent) override;
			virtual void CalcCamera(float DeltaTime, struct FMinimalViewInfo& OutResult) override;
		protected:
			void OnResetVR();
			void TriggerClick();
			void TraceForBlock(const FVector& Start, const FVector& End, bool bDrawDebugHelpers);  

- PuzzleBlockGrid： 网格类，作为游戏的框架部分，提供必要模块的初始化工作，并记录分数。它有一部分创建PuzzlePawn的代码中，**计算行数和列数（通过除法和求余实现）**写的比较精辟，在此分析下：  

	void APuzzleBlockGrid::BeginPlay()
	{
	
		Super::BeginPlay();
	
		// Number of blocks
		// Size = 3;
		// BlockSpacing = 300.f;
		const int32 NumBlocks = Size * Size; // 定义网格大小
	
		// Loop to spawn each block
		for(int32 BlockIndex=0; BlockIndex<NumBlocks; BlockIndex++)
		{
			const float XOffset = (BlockIndex/Size) * BlockSpacing; // Divide by dimension 通过除法计算行数
			const float YOffset = (BlockIndex%Size) * BlockSpacing; // Modulo gives remainder 通过求余计算列数
	
			// Make position vector, offset from Grid location
			const FVector BlockLocation = FVector(XOffset, YOffset, 0.f) + GetActorLocation();
	
			// Spawn a block
			APuzzleBlock* NewBlock = GetWorld()->SpawnActor<APuzzleBlock>(BlockLocation, FRotator(0,0,0));
	
			// Tell the block about its owner
			if (NewBlock != nullptr)
			{
				NewBlock->OwningGrid = this;
			}
		}
	}

- PuzzleController: 玩家控制器类。