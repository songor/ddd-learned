# DDD 实战课

### 开篇词 | 学好了 DDD，你能做什么？

***我与 DDD***

作为中台，需要将通用的可复用的业务能力沉淀到中台业务模型，实现企业级能力复用。因此中台面临的首要问题就是中台领域模型的重构。而中台落地时，依然会面临微服务设计和拆分的问题。

***关于专栏***

中台本质是业务模型，微服务是业务模型的系统落地，DDD 是一种设计思想，它可以同时指导中台业务建模和微服务设计，它们之间就是这样的一个铁三角关系。DDD 强调领域模型和微服务设计的一体性，先有领域模型然后才有微服务，而不是脱离领域模型来谈微服务设计。

### 01 | 领域驱动设计：微服务设计为什么要选择 DDD？

***软件架构模式的演进***

第一阶段是单机架构：采用面向过程的设计方法，系统包括客户端 UI 层和数据库两层，采用 C/S 架构模式，整个系统围绕数据库驱动设计和开发，并且总是从设计数据库和字段开始。

第二阶段是集中式架构：采用面向对象的设计方法，系统包括业务接入层、业务逻辑层和数据库层，采用经典的三层架构，也有部分应用采用传统的 SOA 架构。这种架构容易使系统变得臃肿，可扩展性和弹性伸缩性差。

第三阶段是分布式微服务架构：微服务架构可以很好地实现应用之间的解耦，解决单体应用扩展性和弹性伸缩能力不足的问题。

***微服务设计和拆分的困境***

我认为微服务拆分困境产生的根本原因就是不知道业务或者微服务的边界到底在什么地方。换句话说，确定了业务边界和应用边界，这个困境也就迎刃而解了。

DDD 核心思想是通过领域驱动设计方法定义领域模型，从而确定业务和应用边界，保证业务模型与代码模型的一致性。

***为什么 DDD 适合微服务？***

DDD 是一种处理高度复杂领域的设计思想，它试图分离技术实现的复杂性，并围绕业务概念构建领域模型来控制业务的复杂性，以解决软件难以理解，难以演进的问题。DDD 不是架构，而是一种架构设计方法论，它通过边界划分将复杂业务领域简单化，帮我们设计出清晰的领域和应用边界，可以很容易地实现架构演进。

**DDD 包括战略设计和战术设计两部分：**

战略设计主要从业务视角出发，建立业务领域模型，划分领域边界，建立通用语言的限界上下文，限界上下文可以作为微服务设计的参考边界。

战术设计则从技术视角出发，侧重于领域模型的技术实现，完成软件开发和落地，包括：聚合根、实体、值对象、领域服务、应用服务和资源库等代码逻辑的设计和实现。

*DDD 是如何进行战略设计的：*

DDD 战略设计会建立领域模型，领域模型可以用于指导微服务的设计和拆分。事件风暴是建立领域模型的主要方法，它是一个从发散到收敛的过程。它通常采用用例分析、场景分析和用户旅程分析，尽可能全面不遗漏地分解业务领域，并梳理领域对象之间的关系，这是一个发散的过程。事件风暴过程会产生很多的实体、命令、事件等领域对象，我们将这些领域对象从不同的维度进行聚类，形成如聚合、限界上下文等边界，建立领域模型，这就是一个收敛的过程。

![领域](https://github.com/songor/ddd-learned/blob/master/%E9%A2%86%E5%9F%9F.jpg)

*我们可以用三步来划定领域模型和微服务的边界：*

第一步：在事件风暴中梳理业务过程中的用户操作、事件以及外部依赖关系等，根据这些要素梳理出领域实体等领域对象。

第二步：根据领域实体之间的业务关联性，将业务紧密相关的实体进行组合形成聚合，同时确定聚合中的聚合根、值对象和实体。在这个图里，聚合之间的边界是第一层边界，它们在同一个微服务实例中运行，这个边界是逻辑边界，所以用虚线表示。

第三步：根据业务及语义边界等因素，将一个或者多个聚合划定在一个限界上下文内，形成领域模型。在这个图里，限界上下文之间的边界是第二层边界，这一层边界可能就是未来微服务的边界，不同限界上下文内的领域逻辑被隔离在不同的微服务实例中运行，物理上相互隔离，所以是物理边界，边界之间用实线来表示。

在从业务模型向微服务落地的过程中，也就是从战略设计向战术设计的实施过程中，我们会将领域模型中的领域对象与代码模型中的代码对象建立映射关系，将业务架构和系统架构进行绑定。当我们去响应业务变化调整业务架构和领域模型时，系统架构也会同时发生调整，并同步建立新的映射关系。

***DDD 与微服务的关系***

DDD 是一种架构设计方法，微服务是一种架构风格，两者从本质上都是为了追求高响应力，而从业务视角去分离应用系统建设复杂度的手段。两者都强调从业务出发，其核心要义是强调根据业务发展，合理划分领域边界，持续调整现有架构，优化现有代码，以保持架构和代码的生命力，也就是我们常说的演进式架构。

DDD 主要关注从业务领域视角划分领域边界，构建通用语言进行高效沟通，通过业务抽象建立领域模型，维持业务和代码的逻辑一致性。

微服务主要关注运行时的进程间通信、容错和故障隔离，实现去中心化数据管理和去中心化服务治理，关注微服务的独立开发、测试、构建和部署。

### 02 | 领域、子域、核心域、通用域和支撑域：傻傻分不清？

***如何理解领域和子域？***

在研究和解决业务问题时，DDD 会按照一定的规则将业务领域进行细分，当领域细分到一定的程度后，DDD 会将问题范围限定在特定的边界内，在这个边界内建立领域模型，进而用代码实现该领域模型，解决相应的业务问题。简言之，DDD 的领域就是这个边界内要解决的业务问题域。

既然领域是用来限定业务边界和范围的，那么就会有大小之分，领域越大，业务范围就越大，反之则相反。

领域可以进一步划分为子领域。我们把划分出来的多个子领域称为子域，每个子域对应一个更小的问题域或更小的业务范围。

DDD 的研究方法与自然科学的研究方法类似，当人们在自然科学研究中遇到复杂问题时，通常的做法就是将问题一步一步地细分，再针对细分出来的问题域逐个深入研究，探索和建立所有子域的知识体系。当所有问题子域完成研究时，我们就建立了全部领域的完整知识体系了。

***如何理解核心域、通用域和支撑域？***

子域可以根据自身重要性和功能属性划分为三类子域，它们分别是：核心域、通用域和支撑域。

决定产品和公司核心竞争力的子域是核心域，它是业务成功的主要因素和公司的核心竞争力。没有太多个性化的诉求，同时被多个子域使用的通用功能子域是通用域。还有一种功能子域是必需的，但既不包含决定产品和公司核心竞争力的功能，也不包含通用功能的子域，它就是支撑域。

**那为什么要划分核心域、通用域和支撑域，主要目的是什么呢？**

如果这棵桃树生长在公园里，在园丁的眼里，他喜欢的是“人面桃花相映红”的阳春三月，这时花就是桃树的核心域。但如果这棵桃树生长在果园里，对果农来说，他则是希望在丰收的季节收获硕果累累的桃子，这时果实就是桃树的核心域。

在不同的场景下，不同的人对桃树核心域的理解是不同的，因此对桃树的处理方式也会不一样。

通过领域划分，区分不同子域在公司内的不同功能属性和重要性，从而公司可对不同子域采取不同的资源投入和建设策略，其关注度也会不一样。

### 03 | 限界上下文：定义领域边界的利器

通用语言定义上下文含义，限界上下文则定义领域边界，以确保每个上下文含义在它特定的边界内都具有唯一的含义，领域模型则存在于这个边界之内。

***什么是通用语言？***

在事件风暴过程中，通过团队交流达成共识的，能够简单、清晰、准确描述业务涵义和规则的语言就是通用语言。也就是说，通用语言是团队统一的语言，不管你在团队中承担什么角色，在同一个领域的软件生命周期里都使用统一的语言进行交流。

通用语言包含术语和用例场景，并且能够直接反映在代码中。通用语言中的名词可以给领域对象命名，如商品、订单等，对应实体对象；而动词则表示一个动作或事件，如商品已下单、订单已付款等，对应领域事件或者命令。

**从事件风暴建立通用语言到领域对象设计和代码落地的完整过程：**

在事件风暴的过程中，领域专家会和设计、开发人员一起建立领域模型，在领域建模的过程中会形成通用的业务术语和用户故事。

通过用户故事分析会形成一个个的领域对象，这些领域对象对应领域模型的业务对象，每一个业务对象和领域对象都有通用的名词术语，并且一一映射。

微服务代码模型来源于领域模型，每个代码模型的代码对象跟领域对象一一对应。

设计过程中我们可以用一些表格，来记录事件风暴和微服务设计过程中产生的领域对象及其属性。

![领域对象及其属性](https://github.com/songor/ddd-learned/blob/master/%E9%A2%86%E5%9F%9F%E5%AF%B9%E8%B1%A1%E5%8F%8A%E5%85%B6%E5%B1%9E%E6%80%A7.jpg)

DDD 分析和设计过程中的每一个环节都需要保证限界上下文内术语的统一，在代码模型设计的时侯就要建立领域对象和代码对象的一一映射，从而保证业务模型和代码模型的一致，实现业务语言与代码语言的统一。

***什么是限界上下文？***

我们知道语言都有它的语义环境，同样，通用语言也有它的上下文环境。为了避免同样的概念或语义在不同的上下文环境中产生歧义，DDD 在战略设计上提出了“限界上下文”这个概念，用来确定语义所在的领域边界。

通过领域的限界上下文，我们就可以在统一的领域边界内用统一的语言进行交流。

综合一下，我认为限界上下文的定义就是：用来封装通用语言和领域对象，提供上下文环境，保证在领域之内的一些术语、业务相关对象等（通用语言）有一个确切的含义，没有二义性。这个边界定义了模型的适用范围，使团队所有成员能够明确地知道什么应该在模型中实现，什么不应该在模型中实现。

***进一步理解限界上下文***

限界上下文就是用来细分领域，从而定义通用语言所在的边界。

正如电商领域的商品一样，商品在不同的阶段有不同的术语，在销售阶段是商品，而在运输阶段则变成了货物。同样的一个东西，由于业务领域的不同，赋予了这些术语不同的涵义和职责边界，这个边界就可能会成为未来微服务设计的边界。看到这，我想你应该非常清楚了，领域边界就是通过限界上下文来定义的。

***限界上下文和微服务的关系***

![保险模型](https://github.com/songor/ddd-learned/blob/master/%E4%BF%9D%E9%99%A9%E6%A8%A1%E5%9E%8B.jpg)

领域可以拆分为多个子领域，一个领域相当于一个问题域，领域拆分为子域的过程就是大问题拆分为小问题的过程。在这个图里面保险领域被拆分为：投保、支付、保单管理和理赔四个子域。

子域还可根据需要进一步拆分为子子域，比如，支付子域可继续拆分为收款和付款子子域。拆分到一定程度后，有些子子域的领域边界就可能变成限界上下文的边界了。

子域可能会包含多个限界上下文，如理赔子域就包括报案、查勘和定损等多个限界上下文。也有可能子域本身的边界就是限界上下文边界，如投保子域。

每个领域模型都有它对应的限界上下文，团队在限界上下文内用通用语言交流。领域内所有限界上下文的领域模型构成整个领域的领域模型。

理论上限界上下文就是微服务的边界。我们将限界上下文内的领域模型映射到微服务，就完成了从问题域到软件的解决方案。

***总结***

通用语言确定了项目团队内部交流的统一语言，而这个语言所在的语义环境则是由限界上下文来限定的，以确保语义的唯一性。

而领域专家、架构师和开发人员的主要工作就是通过事件风暴来划分限界上下文。限界上下文确定了微服务的设计和拆分方向，是微服务设计和拆分的主要依据。

### 04 | 实体和值对象：从领域模型的基础单元看系统设计

***实体***

在 DDD 中有这样一类对象，它们拥有唯一标识符，且标识符在历经各种状态变更后仍能保持一致。对这些对象而言，重要的不是其属性，而是其延续性和标识，对象的延续性和标识会跨越甚至超出软件的生命周期。

**实体的业务形态**

领域模型中的实体是多个属性、操作或行为的载体。在事件风暴中，我们可以根据命令、操作或者事件，找出产生这些行为的业务实体对象，进而按照一定的业务规则将依存度高、和业务关联紧密的多个实体对象和值对象进行聚类，形成聚合。

**实体的代码形态**

在代码模型中，实体的表现形式是实体类，这个类包含了实体的属性和方法，通过这些方法实现实体自身的业务逻辑。在 DDD 里，这些实体类通常采用充血模型，与这个实体相关的所有业务逻辑都在实体类的方法中实现，跨多个实体的领域逻辑则在领域服务中实现。

**实体的运行形态**

实体以 DO（领域对象）的形式存在，每个实体对象都有唯一的 ID。我们可以对一个实体对象进行多次修改，修改后的数据和原来的数据可能会大不相同。但是，由于它们拥有相同的 ID，它们依然是同一个实体。

**实体的数据库形态**

与传统数据模型设计优先不同，DDD 是先构建领域模型，针对实际业务场景构建实体对象和行为，再将实体对象映射到数据持久化对象。

在领域模型映射到数据模型时，一个实体可能对应 0 个、1 个或者多个数据库持久化对象。

***值对象***

通过对象属性值来识别的对象，它将多个相关属性组合为一个概念整体。在 DDD 中用来描述领域的特定方面，并且是一个没有标识符的对象，叫作值对象。

也就说，值对象描述了领域中的一件东西，这个东西是不可变的，它将不同的相关属性组合成了一个概念整体。当度量和描述改变时，可以用另外一个值对象予以替换。它可以和其它值对象进行相等性比较，且不会对协作对象造成副作用。

简单来说，值对象本质上就是一个集合。那这个集合里面有什么呢？若干个用于描述目的、具有整体概念和不可修改的属性。那这个集合存在的意义又是什么？在领域建模的过程中，值对象可以保证属性归类的清晰和概念的完整性，避免属性零碎。

**值对象的业务形态**

本质上，实体是看得到、摸得着的实实在在的业务对象，实体具有业务属性、业务行为和业务逻辑。而值对象只是若干个属性的集合，只有数据初始化操作和有限的不涉及修改数据的行为，基本不包含业务逻辑。值对象的属性集虽然在物理上独立出来了，但在逻辑上它仍然是实体属性的一部分，用于描述实体的特征。

在值对象中也有部分共享的标准类型的值对象，它们有自己的限界上下文，有自己的持久化对象，可以建立共享的数据类微服务，比如数据字典。

**值对象的代码形态**

如果值对象是单一属性，则直接定义为实体类的属性；如果值对象是属性集合，则把它设计为 Class 类，Class 将具有整体概念的多个属性归集到属性集合，这样的值对象没有 ID，会被实体整体引用。

**值对象的运行形态**

实体实例化后的 DO 对象的业务属性和业务行为非常丰富，但值对象实例化的对象则相对简单和乏味。除了值对象数据初始化和整体替换的行为外，其它业务行为就很少了。

值对象嵌入到实体，有这样两种不同的数据格式，分别是属性嵌入的方式和序列化大对象的方式。

**值对象的数据库形态**

DDD 引入值对象是希望实现从“数据建模为中心”向“领域建模为中心”转变，减少数据库表的数量和表与表之间复杂的依赖关系，尽可能地简化数据库设计，提升数据库性能。

传统的数据建模大多是根据数据库范式设计的，每一个数据库表对应一个实体，每一个实体的属性值用单独的一列来存储，一个实体主表会对应 N 个实体从表。而值对象在数据库持久化方面简化了设计，它的数据库设计大多采用非数据库范式，值对象的属性值和实体对象的属性值保存在同一个数据库实体表中。

在领域建模时，我们可以把地址作为值对象，人员作为实体，这样就可以保留地址的业务涵义和概念完整性。而在数据建模时，我们可以将地址的属性值嵌入人员实体数据库表中，只创建人员数据库表。这样既可以兼顾业务含义和表达，又不增加数据库的复杂度。

值对象就是通过这种方式简化了数据库设计，总结一下就是：在领域建模时，我们可以将部分对象设计为值对象，保留对象的业务涵义，同时又减少了实体的数量；在数据建模时，我们可以将值对象嵌入实体，减少实体表的数量，简化数据库设计。

**值对象的优势和局限**

值对象采用序列化大对象的方法简化了数据库设计，减少了实体表的数量，可以简单、清晰地表达业务概念。这种设计方式虽然降低了数据库设计的复杂度，但却无法满足基于值对象的快速查询，会导致搜索值对象属性值变得异常困难。

值对象采用属性嵌入的方法提升了数据库的性能，但如果实体引用的值对象过多，则会导致实体堆积一堆缺乏概念完整性的属性，这样值对象就会失去业务含义，操作起来也不方便。

***实体和值对象的关系***

DDD 提倡从领域模型设计出发，而不是先设计数据模型。值对象的诞生，在一定程度上和实体是互补的。

同样的对象在不同的场景下可能会设计出不同的结果。在一些场景中，地址会被某一实体引用，它只承担描述实体的作用，并且它的值只能整体替换，这时候你就可以将地址设计为值对象，比如收货地址。而在另一些场景中，地址会被经常修改，地址是作为一个独立对象存在的，这时候它应该被设计为实体，比如行政区划中的地址信息维护。

### 05 | 聚合和聚合根：怎样设计聚合？

***聚合***

领域模型内的实体和值对象就好比个体，而能让实体和值对象协同工作的组织就是聚合，它用来确保这些领域对象在实现共同的业务逻辑时，能保证数据的一致性。

你可以这么理解，聚合就是由业务和逻辑紧密关联的实体和值对象组合而成的，聚合是数据修改和持久化的基本单元，每一个聚合对应一个仓储，实现数据的持久化。

聚合有一个聚合根和上下文边界，这个边界根据业务单一职责和高内聚原则，定义了聚合内部应该包含哪些实体和值对象，而聚合之间的边界是松耦合的。按照这种方式设计出来的微服务很自然就是“高内聚、低耦合”的。

聚合在 DDD 分层架构里属于领域层，领域层包含了多个聚合，共同实现核心业务逻辑。聚合内实体以充血模型实现个体业务能力，以及业务逻辑的高内聚。跨多个实体的业务逻辑通过领域服务来实现，跨多个聚合的业务逻辑通过应用服务来实现。

***聚合根***

聚合根的主要目的是为了避免由于复杂数据模型缺少统一的业务规则控制，而导致聚合、实体之间数据不一致性的问题。

如果把聚合比作组织，那聚合根就是这个组织的负责人。聚合根也称为根实体，它不仅是实体，还是聚合的管理者。

首先，它作为实体本身，拥有实体的属性和业务行为，实现自身的业务逻辑。

其次，它作为聚合的管理者，在聚合内部负责协调实体和值对象按照固定的业务规则协同完成业务逻辑。

最后，在聚合之间，它还是聚合对外的接口人，以聚合根 ID 关联的方式接受外部任务和请求，在上下文内实现聚合之间的业务协同。也就是说，聚合之间通过聚合根 ID 关联引用，如果需要访问其它聚合的实体，就要先访问聚合根，再导航到聚合内部实体，外部对象不能直接访问聚合内实体。

***怎样设计聚合？***

DDD 领域建模通常采用事件风暴，它通常采用用例分析、场景分析和用户旅程分析等方法，通过头脑风暴列出所有可能的业务行为和事件，然后找出产生这些行为的领域对象，并梳理领域对象之间的关系，找出聚合根，找出与聚合根业务紧密关联的实体和值对象，再将聚合根、实体和值对象组合，构建聚合。

![聚合的构建过程](https://github.com/songor/ddd-learned/blob/master/%E8%81%9A%E5%90%88%E7%9A%84%E6%9E%84%E5%BB%BA%E8%BF%87%E7%A8%8B.jpg)

第 1 步：采用事件风暴，根据业务行为梳理出在投保过程中发生这些行为的所有实体和值对象。

第 2 步：从众多实体中选出适合作为对象管理者的根实体，也就是聚合根。判断一个实体是否是聚合根，你可以结合以下场景分析：是否有独立的生命周期？是否有全局唯一 ID？是否可以创建或修改其它对象？是否有专门的模块来管这个实体。

第 3 步：根据业务单一职责和高内聚原则，找出与聚合根关联的所有紧密依赖的实体和值对象。构建出包含聚合根（唯一）、多个实体和值对象的对象集合，这个集合就是聚合。

第 4 步：在聚合内根据聚合根、实体和值对象的依赖关系，画出对象的引用和依赖模型。

第 5 步：多个聚合根据业务语义和上下文一起划分到同一个限界上下文内。

***聚合的一些设计原则***

**在一致性边界内建模真正的不变条件：**聚合用来封装真正的不变性，而不是简单地将对象组合在一起。聚合内有一套不变的业务规则，各实体和值对象按照统一的业务规则运行，实现对象数据的一致性，边界之外的任何东西都与该聚合无关，这就是聚合能实现业务高内聚的原因。

**设计小聚合：**如果聚合设计得过大，聚合会因为包含过多的实体而导致实体之间的管理过于复杂，高频操作时会出现并发冲突或者数据库锁，最终导致系统可用性变差。而小聚合设计则可以降低由于业务过大导致聚合重构的可能性，让领域模型更能适应业务的变化。

**通过唯一标识引用其它聚合：**聚合之间是通过关联外部聚合根 ID 的方式引用，而不是直接引用对象。外部聚合的对象放在聚合边界内管理，容易导致聚合的边界不清晰，也会增加聚合之间的耦合度。

**在边界之外使用最终一致性：**聚合内数据强一致性，而聚合之间数据最终一致性。在一次事务中，最多只能更改一个聚合的状态。如果一次业务操作涉及多个聚合状态的更改，应采用领域事件的方式异步修改相关的聚合，实现聚合之间的解耦。

**通过应用层实现跨聚合的服务调用：**为实现微服务内聚合之间的解耦，以及未来以聚合为单位的微服务组合和拆分，应避免跨聚合的领域服务调用和跨聚合的数据库表关联。

### 06 | 领域事件：解耦微服务的关键

***领域事件***

在事件风暴中，我们发现除了命令和操作等业务行为以外，还有一种非常重要的事件，这种事件发生后通常会导致进一步的业务操作，在 DDD 中这种事件被称为领域事件。

**那如何识别领域事件呢？**

在做用户旅程或者场景分析时，我们要捕捉业务、需求人员或领域专家口中的关键词：“如果发生...，则...”，“当做完...的时候，请通知...”等。

领域事件驱动设计可以切断领域模型之间的强依赖关系，事件发布完成后，发布方不必关心后续订阅方事件是否处理成功，这样可以实现领域模型的解耦，维护领域模型的独立性和数据的一致性。在领域模型映射到微服务系统架构时，领域事件可以解耦微服务，微服务之间的数据不必要求强一致性，而是基于事件的最终一致性。

**在微服务设计时不同领域事件的处理方式会不一样：**

*微服务内的领域事件*

当领域事件发生在微服务内的聚合之间，领域事件发生后完成事件实体构建和事件数据持久化，发布方聚合将事件发布到事件总线，订阅方接收事件数据完成后续业务操作。

微服务内大部分事件的集成都发生在同一个进程内，进程自身可以很好地控制事务，因此不一定需要引入消息中间件。但如果一个事件同时更新多个聚合，按照 DDD “一次事务只更新一个聚合”的原则，你就要考虑是否引入事件总线。微服务内的事件总线可能会增加开发的复杂度，因此你需要结合应用复杂度和收益进行综合考虑。

微服务内应用服务可以通过跨聚合的服务编排和组合，以服务调用的方式完成跨聚合的访问，这种方式通常应用于实时性和数据一致性要求高的场景。

*微服务间的领域事件*

跨微服务的领域事件会在不同的限界上下文或领域模型之间实现业务协作，其主要目的是实现微服务解耦，减轻微服务之间实时访问的压力。

跨微服务的事件可以推动业务流程或者数据在不同的子域或微服务间直接流转。

跨微服务的事件机制要总体考虑事件构建、发布和订阅、事件数据持久化、消息中间件，甚至事件数据持久化时还可能需要考虑引入分布式事务机制等。

微服务之间的访问也可以采用应用服务直接调用的方式，实现数据和服务的实时访问，弊端就是跨微服务的数据同时变更需要引入分布式事务，以确保数据的一致性。分布式事务机制会影响系统性能，增加微服务之间的耦合，所以我们还是要尽量避免使用分布式事务。

***领域事件相关案例***

![用领域事件驱动设计来驱动承保业务流程](https://github.com/songor/ddd-learned/blob/master/%E7%94%A8%E9%A2%86%E5%9F%9F%E4%BA%8B%E4%BB%B6%E9%A9%B1%E5%8A%A8%E8%AE%BE%E8%AE%A1%E6%9D%A5%E9%A9%B1%E5%8A%A8%E6%89%BF%E4%BF%9D%E4%B8%9A%E5%8A%A1%E6%B5%81%E7%A8%8B.jpg)

***领域事件总体架构***'

![领域事件处理机制](https://github.com/songor/ddd-learned/blob/master/%E9%A2%86%E5%9F%9F%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E6%9C%BA%E5%88%B6.jpg)

领域事件处理包括：事件构建和发布、事件数据持久化、事件总线、消息中间件、事件接收和处理等。

**事件构建和发布**

事件基本属性至少包括：事件唯一标识、发生时间、事件类型和事件源，其中事件唯一标识应该是全局唯一的，以便事件能够无歧义地在多个限界上下文中传递。

另外事件中还有一项更重要，那就是业务属性，用于记录事件发生那一刻的业务数据，这些数据会随事件传输到订阅方，以开展下一步的业务操作。

领域事件发生后，事件中的业务数据不再修改，因此业务数据可以以序列化值对象的形式保存，这种存储格式在消息中间件中也比较容易解析和获取。

为了保证事件结构的统一，我们还会创建事件基类 DomainEvent，子类可以扩充属性和方法。

事件发布之前需要先构建事件实体并持久化。事件发布的方式有很多种，你可以通过应用服务或者领域服务发布到事件总线或者消息中间件，也可以从事件表中利用定时程序或数据库日志捕获技术获取增量事件数据，发布到消息中间件。

**事件数据持久化**

事件数据持久化可用于系统之间的数据对账，或者实现发布方和订阅方事件数据的审计。当遇到消息中间件、订阅方系统宕机或者网络中断，在问题解决后仍可继续后续业务流转，保证数据的一致性。

事件数据持久化有两种方案：

持久化到本地业务数据库的事件表中，利用本地事务保证业务和事件数据的一致性。

持久化到共享的事件数据库中。这里需要注意的是，业务数据库和事件数据库不在一个数据库中，它们的数据持久化操作会跨数据库，因此需要分布式事务机制来保证业务和事件数据的强一致性，结果就是会对系统性能造成一定的影响。

**事件总线**

事件总线是实现微服务内聚合之间领域事件的重要组件，它提供事件分发和接收等服务。事件总线是进程内模型，它会在微服务内聚合之间遍历订阅者列表，采取同步或异步的模式传递数据。

如果是微服务内的订阅者（其它聚合），则直接分发到指定订阅者；如果是微服务外的订阅者，将事件数据保存到事件库（表）并异步发送到消息中间件；如果同时存在微服务内和外订阅者，则先分发到内部订阅者，将事件消息保存到事件库（表），再异步发送到消息中间件。

事件总线可以理解为运行在同一个进程内的消息中间件，它是一个很小的技术组件，可以通过配置支持异步或同步的消息机制。

**消息中间件**

跨微服务的领域事件大多会用到消息中间件，实现跨微服务的事件发布和订阅。

**事件接收和处理**

微服务订阅方在应用层采用监听机制，接收消息队列中的事件数据，完成事件数据的持久化后，就可以开始进一步的业务处理。

***领域事件运行机制相关案例***

![领域事件运行机制案例](https://github.com/songor/ddd-learned/blob/master/%E9%A2%86%E5%9F%9F%E4%BA%8B%E4%BB%B6%E8%BF%90%E8%A1%8C%E6%9C%BA%E5%88%B6%E6%A1%88%E4%BE%8B.jpg)

### 07 | DDD 分层架构：有效降低层与层之间的依赖

***什么是 DDD 分层架构？***

![DDD 分层架构](https://github.com/songor/ddd-learned/blob/master/DDD%20%E5%88%86%E5%B1%82%E6%9E%B6%E6%9E%84.jpg)

**用户接口层**

用户接口层负责向用户显示信息和解释用户指令。这里的用户可能是：用户、程序、自动化测试和批处理脚本等等。

**应用层**

应用层是很薄的一层，理论上不应该有业务规则或逻辑，主要是面向用例和流程相关的操作。但应用层又位于领域层之上，因为领域层包含多个聚合，所以它可以协调多个聚合的服务和领域对象完成服务编排和组合，协作完成业务操作。

此外，应用层也是微服务之间交互的通道，它可以调用其它微服务的应用服务，完成微服务之间的服务组合和编排。

应用服务是在应用层的，它负责服务的组合、编排和转发，负责处理业务用例的执行顺序以及结果的拼装，以粗粒度的服务通过 API 网关向前端发布。还有，应用服务还可以进行安全认证、权限校验、事务控制、发送或订阅领域事件等。

**领域层**

领域层主要体现领域模型的业务能力，它用来表达业务概念、业务状态和业务规则。

领域层包含聚合根、实体、值对象、领域服务等领域模型中的领域对象。

首先，领域模型的业务逻辑主要是由实体和领域服务来实现的，其中实体会采用充血模型来实现所有与之相关的业务功能。其次，实体和领域服务在实现业务逻辑上不是同级的，当领域中的某些功能在单一实体（或者值对象）中不能实现时，领域服务就会出马，它可以组合聚合内的多个实体（或者值对象），实现复杂的业务逻辑。

**基础层**

基础层是贯穿所有层的，它的作用就是为其它各层提供通用的技术和基础服务，包括第三方工具、驱动、消息中间件、网关、文件、缓存以及数据库等。

基础层包含基础服务，它采用依赖倒置设计，封装基础资源服务，实现应用层、领域层与基础层的解耦，降低外部资源变化对应用的影响。

***DDD 分层架构最重要的原则是什么？***

每层只能与位于其下方的层发生耦合。

在严格分层架构中，领域服务只能被应用服务调用，而应用服务只能被用户接口层调用，服务是逐层对外封装或组合的，依赖关系清晰。

***DDD 分层架构如何推动架构演进？***

**微服务架构的演进**

![微服务架构的演进](https://github.com/songor/ddd-learned/blob/master/%E5%BE%AE%E6%9C%8D%E5%8A%A1%E6%9E%B6%E6%9E%84%E7%9A%84%E6%BC%94%E8%BF%9B.jpg)

聚合内业务功能内聚，能独立完成特定的业务逻辑。聚合的重组或拆分，势必就会引起业务模块和系统功能的变化。

我们可以以聚合为基础单元，完成领域模型和微服务架构的演进。聚合可以作为一个整体，在不同的领域模型之间重组或者拆分，或者直接将一个聚合独立为微服务。

**微服务内服务的演进**

在微服务内部，实体的方法被领域服务组合和封装，领域服务又被应用服务组合和封装。

![微服务内服务的演进](https://github.com/songor/ddd-learned/blob/master/%E5%BE%AE%E6%9C%8D%E5%8A%A1%E5%86%85%E6%9C%8D%E5%8A%A1%E7%9A%84%E6%BC%94%E8%BF%9B.jpg)

***三层架构如何演进到 DDD 分层架构？***

DDD 分层架构中的要素其实和三层架构类似，只是在 DDD 分层架构中，这些要素被重新归类，重新划分了层，确定了层与层之间的交互规则和职责边界。

![三层架构演进到 DDD 分层架构](https://github.com/songor/ddd-learned/blob/master/%E4%B8%89%E5%B1%82%E6%9E%B6%E6%9E%84%E6%BC%94%E8%BF%9B%E5%88%B0%20DDD%20%E5%88%86%E5%B1%82%E6%9E%B6%E6%9E%84.jpg)

DDD 分层架构在用户接口层引入了 DTO，给前端提供了更多的可使用数据和更高的展示灵活性。

DDD 分层架构将业务逻辑层的服务拆分到了应用层和领域层，应用层快速响应前端的变化，领域层实现领域模型的能力。

三层架构数据访问采用 DAO 方式，DDD 分层架构的数据库等基础资源访问采用了仓储（Repository）设计模式，通过依赖倒置实现各层对基础资源的解耦。

仓储又分为两部分，仓储接口和仓储实现，仓储接口放在领域层，仓储实现放在基础层。

***补充***

**MapperXML**

是 Mybatis 的映射文件。仓储本身是属于基础层，但是考虑到一个聚合对应一个仓储，为了方便以后整体迁移聚合代码，在微服务代码目录设计时，增加了一个 Repository 的仓储目录，跟仓储相关的代码都放在这个目录下。

如果未来换数据库的话，只需要将 Repository 目录下的代码替换就可以了。而如果聚合需要整体迁移到其它微服务中去，仓储的代码也会一并迁移。

**Application Service 和 Domain Service**

单个实体自身的方法就是实体本身的业务行为，多个实体可组成更复杂的业务动作，这个是领域服务，实体的方法和领域服务共同构成领域模型的基础业务能力，这个能力是原子的、基础的，不太考虑外界的用户行为和流程。而应用服务是对这些基础的能力进行组合和编排，它组合和编排的服务可以是跨聚合的领域服务，主要体现组合后的业务能力，更面向前端的用户操作，属于比较粗粒度的服务，通过编排可以更灵活应对外部需求变化。