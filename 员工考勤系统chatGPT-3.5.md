# 第四章：用例建模

*[综合案例:员工考勒系统]
现要为某单位开发一款“ 员工考勤系统”，其开发背景和问题陈述如下。根据该系统陈述和对相关业务的理解，完成系统用例图和核心用例的用例文档。*

*作为Acme公司的信息主管，你被委托开发一款新的考勤系统 。要求新系统允许员工记录电子的考勤信息并自动产生员工的工资支付信息。*

*新系统运行在整个公司内部的每名员工的计算机上，考虑到安全和隐私方面的原因，每名员工只能访问和编辑自己的考勤信息和工资支付信息,但是项目经理可以查看和编辑本项目组内部所有员工的信息。*

*新系统用于维护公司内部所有的员工信息(目前公司大约有5000多名员工)，系统必须能够按照员工的考勤信息按时正确地计算工资信息。由于费用原因，目前公司并不打算替换已有的遗留数据库系统一项目管理数据库。在该数据库中保存着公司所有的项目信息及相关的工资级别代码,属于不同项目的员工，其工资的计算方式并不相同(根据工资级别代码来区分)。该数据库采用的是运行在IBM主机上的DB2系统。考勤系统需要访问该数据库的信息,但不进行更新操作。*

*公司内部按项目组的形式管理，项目经理负责整个项目组;而组内一.般存在3类雇员。*

*第一类为小时工,其工资按照小时计算。他们每天需要记录当天的工作小时，根据工作时间和所属项目的工资级别代码来计算当天的工资;如果当天工作超过8小时，则超过的部分按加班计算(工资为平时的1.5倍)。这类员工每周五结算本周工资。*

*第二类为普通员工，其工资每月固定。为了跟踪他们的上班情况，他们每天也需要记录当天的工作时间，某些项目组可能会根据该工作时间对员工进行奖惩(具体奖惩措施本系统不处理，由项目经理自行决定)。这类员工每个月末结算工资。*

*第三类为销售人员,这类员工不用每天记录考勤信息，而是记录当天完成的订单情况。其工资的计算方式是根据当月的订单情况进行提成。根据订单的性质不同，提成的比例也有所差别，具体提成比例有5%、10%、15%、25%这4个档次。这类员工工资也是在每个月末结算。*

*新系统另一个最重要的特征就是所有的员工可以随时查看自己的考勤信息，对于员工而言，提交的考勤信息不允许修改(如果实在存在错误，可由项目经理修改):在每个月末(对于小时工则为每个周末)，还可以查看自己本月的工资支付信息(以前的工资信息可随时查看)。*

*为了保证员工能够及时地获得本月的工资情况，该系统在每个周五和每个月末会自动运行，为员工产生相应的工资信息，并及时提醒项目经理确认工资信息。经项目经理确认后的工资信息即可公开给员工。*

## (1)用例图

绘制员工考勤系统的用例图时，首先要识别系统的参与者和用例。以下是可能出现在员工考勤系统用例图中的参与者和用例的示例：

**参与者：**

1. 员工： 使用系统记录考勤信息、查看工资信息。
2. 项目经理： 负责查看和编辑项目组内员工的考勤信息，确认工资信息。

**用例：**

1. 记录考勤信息：

   - 员工录入考勤信息
   - 项目经理查看和编辑考勤信息
2. 生成工资信息：

   - 系统自动运行生成工资信息
   - 项目经理确认工资信息
3. 查看考勤信息：

   - 员工查看考勤信息
   - 项目经理查看和编辑考勤信息
4. 查看工资支付信息：

   - 员工查看工资支付信息
   - 项目经理查看和编辑工资信息

**用例图示例：**

```plaintext
+---------------------+
| 员工考勤系统      |
+---------------------+
        |
        | 1. 记录考勤信息
        |---------------------|
        |                     |
        v                     v
+--------------+   +------------------+
|  员工        |   |  项目经理         |
+--------------+   +------------------+
| 录入考勤信息  |   | 查看和编辑考勤信息  |
| 查看考勤信息  |   | 确认工资信息        |
| 查看工资信息  |   | 查看和编辑工资信息  |
+--------------+   +------------------+
```

在用例图中，椭圆形表示用例，方框表示参与者。实线箭头表示参与者与用例之间的关系，箭头指向用例表示参与者与该用例有交互。这个简单的用例图描述了员工考勤系统的主要功能和参与者之间的关系。

## (2)核心用例文档

**1. 记录考勤信息**

- 参与者： 员工、项目经理
- 目标： 允许员工记录每天的考勤信息。
- 前提条件： 员工登录系统。
- 描述：
  - 员工可以录入每天的工作小时或完成的订单情况。
  - 项目经理可以查看和编辑本项目组内员工的考勤信息。

**2. 生成工资信息**

- 参与者： 系统、项目经理
- 目标： 根据员工的考勤信息和工资级别代码，生成工资支付信息。
- 前提条件： 每个周五和每个月末系统自动运行。
- 描述：
  - 对于小时工，系统根据工作小时和工资级别代码计算工资，超过8小时的部分按加班计算。
  - 对于普通员工，系统根据工作时间和工资级别代码计算工资。
  - 对于销售人员，系统根据订单情况和提成比例计算工资。

**3. 查看考勤信息**

- 参与者： 员工
- 目标： 允许员工查看自己的考勤信息。
- 前提条件： 员工登录系统。
- 描述：
  - 员工可以随时查看自己录入的考勤信息。
  - 提交的考勤信息不允许员工修改，但可由项目经理修改。

**4. 查看工资支付信息**

- 参与者： 员工
- 目标： 允许员工查看每月的工资支付信息。
- 前提条件： 每个月末或周末。
- 描述：
  - 员工可以在每月末查看本月的工资支付信息。
  - 员工可以随时查看以前的工资支付信息。

**5. 项目经理确认工资信息**

- 参与者： 项目经理
- 目标： 允许项目经理确认员工的工资信息。
- 前提条件： 生成工资信息后。
- 描述：
  - 项目经理可以查看和编辑本项目组内员工的工资信息。
  - 项目经理确认后的工资信息可公开给员工。

**6. 维护员工信息**

- 参与者： 系统管理员
- 目标： 允许管理员维护员工信息。
- 前提条件： 系统管理员登录系统。
- 描述：
  - 添加、删除、编辑员工的基本信息。
  - 更新员工的工资级别代码。

## (3)补充说明

- 本系统采用现有的遗留数据库系统，不进行更新操作。
- 每个周五和每个月末系统自动运行，生成相应的工资信息。
- 提交的考勤信息不允许员工修改，但可以由项目经理修改。
- 具体的奖惩措施由项目经理自行决定，本系统不处理。
- 销售人员的提成比例分别有5%、10%、15%、25%这4个档次，根据订单的性质不同而定。

# 第五章：用例分析

***[综合案例:员工考勤系统]***

*在第4章已经完成的该系统用例模型基础上，完成分析过程。*

*(1 )简单描述系统的备选构架,并将分析过程所发现的类放人到相应的层次结构中。*

*(2)针对系统的核心用例，完成用例分析工作，每个用例实现模型至少应包括:*

*(2.1)描述基本路径的交互*

*(2.2)用例实现的参与类类图*

*(3)构造系统完整的实体类类图。*

## (1) 系统备选构架和类层次结构

**备选构架：**

- 前端应用层： 包括员工和项目经理的界面，用于记录考勤信息和查看工资信息。
- 业务逻辑层： 处理核心业务逻辑，包括生成工资信息、项目经理确认等。
- 数据访问层： 与遗留数据库系统进行交互，获取员工和项目信息。

**类层次结构：**

1. 前端应用层：

   - EmployeeUI： 员工界面类
   - ProjectManagerUI： 项目经理界面类
2. 业务逻辑层：

   - AttendanceSystem： 主系统类，负责调度各个业务功能。
   - EmployeeManager： 员工管理类，处理员工信息和考勤记录。
   - SalaryCalculator： 工资计算类，根据考勤信息和工资级别计算工资。
   - ConfirmationManager： 确认管理类，处理项目经理确认工资信息的逻辑。
3. 数据访问层：

   - LegacyDatabaseAccessor： 遗留数据库访问类，用于获取项目和工资级别信息。

## (2) 用例分析

### 2.1 描述基本路径的交互

**记录考勤信息：**

1. 员工录入考勤信息：

   - EmployeeUI 提供界面，EmployeeManager 处理录入请求，记录考勤信息。
2. 项目经理查看和编辑考勤信息：

   - ProjectManagerUI 提供界面，EmployeeManager 处理查看和编辑请求。

**生成工资信息：**

1. 系统自动运行生成工资信息：

   - AttendanceSystem 调用 SalaryCalculator 计算工资，LegacyDatabaseAccessor 获取工资级别信息。
2. 项目经理确认工资信息：

   - ProjectManagerUI 提供界面，ConfirmationManager 处理确认请求。

**查看考勤信息：**

1. 员工查看考勤信息：

   - EmployeeUI 提供界面，EmployeeManager 处理查看请求。
2. 项目经理查看和编辑考勤信息：

   - ProjectManagerUI 提供界面，EmployeeManager 处理查看和编辑请求。

**查看工资支付信息：**

1. 员工查看工资支付信息：

   - EmployeeUI 提供界面，SalaryCalculator 获取工资信息，EmployeeManager 处理展示。
2. 项目经理查看和编辑工资信息：

   - ProjectManagerUI 提供界面，ConfirmationManager 处理查看和编辑请求。

### 2.2 用例实现的参与类类图

用例实现的参与类类图描述了系统中用例的实现和各个类之间的关系。在这个情境下，我们可以关注用例的实现，以及用于支持这些用例的类。以下是一个简单的员工考勤系统用例实现的参与类类图示例：

**用例实现的参与类类图示例：**

```plaintext
+---------------------+
|  员工考勤系统实现   |
+---------------------+
        |
        | 1. 记录考勤信息
        |---------------------|
        |                     |
        v                     v
+-----------------------+ +--------------------+
|  员工                 | |  项目经理           |
+-----------------------+ +--------------------+
| EmployeeUI            | | ProjectManagerUI   |
| EmployeeManager       | | ConfirmationManager|
| SalaryCalculator      | |                    |
| LegacyDatabaseAccessor| |                    |
+-----------------------+ +--------------------+
```

在上面的类图中：

- `EmployeeUI` 和 `ProjectManagerUI` 是用于记录考勤信息和查看工资信息的用户界面类。
- `EmployeeManager` 处理员工信息和考勤记录的业务逻辑。
- `SalaryCalculator` 负责计算工资的业务逻辑。
- `ConfirmationManager` 处理项目经理确认工资信息的业务逻辑。
- `LegacyDatabaseAccessor` 与遗留数据库系统进行交互，获取项目和工资级别信息。

箭头表示类之间的关系，例如，`EmployeeManager` 类使用了 `LegacyDatabaseAccessor` 类来获取数据库信息，`EmployeeUI` 类使用了 `EmployeeManager` 类来进行考勤信息的录入和查看。

这个类图是一个简单的示例，实际的类图可能更加复杂，具体的设计取决于系统的具体需求和架构。

## (3) 实体类类图

实体类类图描述了系统中的实体（Entity）以及它们之间的关系。在员工考勤系统中，实体类通常对应系统中的数据对象，比如员工、考勤记录、工资记录等。以下是一个简单的员工考勤系统实体类类图示例：

**实体类类图示例：**

```plaintext
+---------------------+
|    员工考勤系统      |
+---------------------+
        |
+--------------+
|   Employee   |
+--------------+
| - EmployeeID : int  |
| - Name : string     |
| - Position : string |
| - Type : string     |
| ...                |
+--------------+
        |
        | 1            * 
        |
+--------------+
|  Attendance  |
+--------------+
| - AttendanceID : int |
| - Date : Date       |
| - HoursWorked : decimal |
| - OrderCount : int   |
| ...                |
+--------------+
        |
        | 1            *
        |
+------------------+
|  SalaryRecord   |
+------------------+
| - RecordID : int  |
| - Date : Date     |
| - Amount : decimal|
| - Status : string |
| ...              |
+------------------+
```

在上面的类图中：

- `Employee` 类表示员工实体，包含了员工的基本信息（EmployeeID、Name、Position、Type等）。
- `Attendance` 类表示考勤记录实体，包含了考勤记录的基本信息（AttendanceID、Date、HoursWorked、OrderCount等）。
- `SalaryRecord` 类表示工资记录实体，包含了工资记录的基本信息（RecordID、Date、Amount、Status等）。
- 关系线（1 *）表示一个员工可以对应多个考勤记录和工资记录。

这个实体类类图简单地表示了员工、考勤记录和工资记录之间的关系，其中每个实体类包含了与之相关的属性。在实际应用中，可能还有其他实体和关系需要考虑，具体取决于系统的复杂性和需求。

## (4)补充说明：

- 在前端应用层，EmployeeUI 和 ProjectManagerUI 负责处理界面逻辑，与业务逻辑层交互。
- 业务逻辑层中，AttendanceSystem 调度 EmployeeManager 处理员工信息和考勤记录，调用 SalaryCalculator 计算工资，调用 ConfirmationManager 处理项目经理确认工资信息。
- 数据访问层中，LegacyDatabaseAccessor 与遗留数据库系统进行交互，获取项目和工资级别信息。
- 实体类包括 Employee（员工）、Project（项目）和SalaryRecord（工资记录）等。 Employee 类中包含了不同类型员工的特定信息。

# 第八章：架构设计

*[综合案例:员工考勤系统]*

*结合已经完成的需求和分析模型，以本章介绍的架构设计方法,设计该系统架构。*

## (1)系统架构设计

**1. 三层架构**

为了实现系统的松耦合和可维护性，采用三层架构：

- 表示层（Presentation Layer）：

  - 前端应用层，包括员工界面（EmployeeUI）和项目经理界面（ProjectManagerUI）。
  - 使用现代的Web框架或前端库，如React或Angular，实现友好的用户界面。
- 业务逻辑层（Business Logic Layer）：

  - 主要包括 AttendanceSystem、EmployeeManager、SalaryCalculator 和 ConfirmationManager 等类。
  - AttendanceSystem 作为业务逻辑的调度中心，协调各个业务逻辑的运行。
  - 使用面向对象的编程语言（如Java或C#）实现业务逻辑。
- 数据访问层（Data Access Layer）：

  - LegacyDatabaseAccessor 负责与遗留数据库系统进行交互，获取项目和工资级别信息。
  - 使用数据库访问框架（如Hibernate或Entity Framework）处理数据访问。

**2. 架构图**

绘制系统架构图是为了显示系统的整体结构，包括不同模块或层次之间的关系。在员工考勤系统中，我们可以采用三层架构，包括表示层（Presentation Layer）、业务逻辑层（Business Logic Layer）和数据访问层（Data Access Layer）。以下是一个简单的员工考勤系统架构图示例：

员工考勤系统架构图示例：

```plaintext
+------------------------+
|   Employee Attendance  |
|        System          |
+------------------------+
        |
+------------------------+
|   Presentation Layer   |
+------------------------+
        |
+--------------+    +--------------+
| EmployeeUI  |    | ProjectManager|
| ProjectManagerUI |  |    UI        |
+--------------+    +--------------+
        |
+------------------------+
|  Business Logic Layer  |
+------------------------+
        |
+----------------+    +------------------+
| AttendanceSystem|    | EmployeeManager  |
| SalaryCalculator|    | ConfirmationManager|
+----------------+    +------------------+
        |
+------------------------+
|   Data Access Layer    |
+------------------------+
        |
+------------------------+
| LegacyDatabaseAccessor |
+------------------------+
```

在这个架构图中：

- 表示层（Presentation Layer）：

  - 包括员工界面 (`EmployeeUI`) 和项目经理界面 (`ProjectManagerUI`)。
  - 负责接收用户输入，展示信息，并将用户请求传递给业务逻辑层。
- 业务逻辑层（Business Logic Layer）：

  - 包括 `AttendanceSystem` 作为业务逻辑的调度中心，以及 `EmployeeManager`、`SalaryCalculator` 和 `ConfirmationManager` 等模块。
  - `AttendanceSystem` 协调各个业务逻辑的运行。
  - `EmployeeManager` 处理员工信息和考勤记录的业务逻辑。
  - `SalaryCalculator` 处理工资计算的业务逻辑。
  - `ConfirmationManager` 处理项目经理确认工资信息的业务逻辑。
- 数据访问层（Data Access Layer）：

  - 包括 `LegacyDatabaseAccessor` 模块，负责与遗留数据库系统进行交互，获取项目和工资级别信息。

箭头表示模块之间的依赖关系，即一个模块可能调用另一个模块的功能。这个简单的三层架构图显示了系统整体结构，有助于理解不同层次之间的关系。在实际应用中，架构图可能更加详细，具体的设计取决于系统的需求和规模。

**3. 模块详细说明**

- 前端应用层模块：

  - EmployeeUI Module： 实现员工界面，包括记录考勤信息和查看工资信息的功能。
  - ProjectManagerUI Module： 实现项目经理界面，包括查看和编辑员工考勤信息以及确认工资信息的功能。
- 业务逻辑层模块：

  - AttendanceSystem Module： 负责协调各业务逻辑的运行，接收前端请求并调用相应的业务逻辑。
  - EmployeeManager Module： 处理员工信息和考勤记录的业务逻辑，包括录入和查看考勤信息。
  - SalaryCalculator Module： 实现工资计算的业务逻辑，根据考勤信息和工资级别计算工资。
  - ConfirmationManager Module： 处理项目经理确认工资信息的业务逻辑。
- 数据访问层模块：

  - LegacyDatabaseAccessor Module： 与遗留数据库系统交互，获取项目和工资级别信息。

**4. 模块间交互**

- 前端应用层与业务逻辑层：

  - EmployeeUI 和 ProjectManagerUI 通过定义的接口向 AttendanceSystem 发送请求，获取业务逻辑的处理结果。
- 业务逻辑层与数据访问层：

  - AttendanceSystem 调用 LegacyDatabaseAccessor 获取项目和工资级别信息，以支持工资计算和确认操作。

**5. 安全性考虑**

- 身份验证和授权：

  - 使用身份验证机制确保只有合法用户可以访问系统。
  - 基于角色的授权，确保不同角色有不同的权限，如员工只能访问自己的信息，而项目经理可以访问整个项目组的信息。
- 数据隐私：

  - 采用加密技术保护敏感数据的传输和存储，确保数据隐私不被泄露。
- 防止SQL注入：

  - 在数据访问层使用参数化查询，以防止SQL注入攻击。

**6. 可扩展性和可维护性**

- 模块化设计：

  - 每个模块独立设计，易于理解和维护。
  - 采用接口和抽象类，实现模块之间的松耦合。
- 插件式架构：

  - 设计支持插件式扩展，以便将来添加新的业务逻辑或改进现有功能。
- 日志记录：

  - 引入日志记录机制，记录系统运行时的关键事件，便于故障排查和性能优化。

## (2)总结

通过采用三层架构，系统得到了合理的划分和组织，使得每个模块的职责清晰，易于维护和扩展。同时，引入了安全性考虑和可扩展性设计，确保系统在运行过程中是安全、可靠且具备良好的扩展性。



# 第九章：构建设计

*[综合案例:员工考勤系统]*

*基于已经完成的分析和设计工作，完成该系统的构件设计。*

*(1))针对系统的核心用例，完成用例设计工作.每个用例实现模型至少应包括:*

*1.1描述基本路径的交互*

*1.2用例实现的参与类类图*

*(2)完成系统的数据库设计。*

## (1) 用例设计

**1. 记录考勤信息**

1.1 描述基本路径的交互

1. 员工录入考勤信息：

   - EmployeeUI 提供录入考勤信息的界面。
   - EmployeeManager 处理录入请求，验证权限后将考勤信息存储。
2. 项目经理查看和编辑考勤信息：

   - ProjectManagerUI 提供查看和编辑考勤信息的界面。
   - EmployeeManager 处理查看和编辑请求，验证权限后返回或更新考勤信息。

1.2 用例实现的参与类类图


**2. 生成工资信息**

1.1 描述基本路径的交互

1. 系统自动运行生成工资信息：

   - AttendanceSystem 触发自动运行，调用 SalaryCalculator 计算工资。
   - SalaryCalculator 使用 LegacyDatabaseAccessor 获取工资级别信息，计算并存储工资。
2. 项目经理确认工资信息：

   - ProjectManagerUI 提供确认工资信息的界面。
   - ConfirmationManager 处理确认请求，验证权限后更新工资信息状态。

1.2 用例实现的参与类类图


**3. 查看考勤信息**

1.1 描述基本路径的交互

1. 员工查看考勤信息：

   - EmployeeUI 提供查看考勤信息的界面。
   - EmployeeManager 处理查看请求，返回相应的考勤信息。
2. 项目经理查看和编辑考勤信息：

   - ProjectManagerUI 提供查看和编辑考勤信息的界面。
   - EmployeeManager 处理查看和编辑请求，验证权限后返回或更新考勤信息。

1.2 用例实现的参与类类图


**4. 查看工资支付信息**

1.1 描述基本路径的交互

1. 员工查看工资支付信息：

   - EmployeeUI 提供查看工资支付信息的界面。
   - SalaryCalculator 获取工资信息，EmployeeManager 处理展示请求。
2. 项目经理查看和编辑工资信息：

   - ProjectManagerUI 提供查看和编辑工资信息的界面。
   - ConfirmationManager 处理查看和编辑请求，验证权限后返回或更新工资信息。

1.2 用例实现的参与类类图


## (2) 系统数据库设计

**1. 实体关系图**

根据系统需求和分析，设计以下实体关系图：


**2. 表结构设计**

2.1 Employee 表（员工信息）

| 字段名     | 数据类型     | 描述                                   |
| ---------- | ------------ | -------------------------------------- |
| EmployeeID | INT          | 员工ID（主键）                         |
| Name       | VARCHAR(100) | 员工姓名                               |
| Position   | VARCHAR(50)  | 员工职位                               |
| Type       | VARCHAR(20)  | 员工类型（小时工、普通员工、销售人员） |
| ...        |              |                                        |

2.2 Attendance 表（考勤信息）

| 字段名       | 数据类型     | 描述                         |
| ------------ | ------------ | ---------------------------- |
| AttendanceID | INT          | 考勤记录ID（主键）           |
| EmployeeID   | INT          | 员工ID（外键）               |
| Date         | DATE         | 考勤日期                     |
| HoursWorked  | DECIMAL(5,2) | 工作小时（小时工和普通员工） |
| OrderCount   | INT          | 订单数量（销售人员）         |
| ...          |              |                              |

2.3 SalaryRecord 表（工资记录）

| 字段名     | 数据类型      | 描述                       |
| ---------- | ------------- | -------------------------- |
| RecordID   | INT           | 工资记录ID（主键）         |
| EmployeeID | INT           | 员工ID（外键）             |
| Date       | DATE          | 工资计算日期               |
| Amount     | DECIMAL(10,2) | 工资金额                   |
| Status     | VARCHAR(20)   | 工资状态（待确认、已确认） |
| ...        |               |                            |

2.4 Project 表（项目信息）

| 字段名    | 数据类型     | 描述           |
| --------- | ------------ | -------------- |
| ProjectID | INT          | 项目ID（主键） |
| Name      | VARCHAR(100) | 项目名称       |
| LevelCode | VARCHAR(10)  | 工资级别代码   |
| ...       |              |                |

**3. 数据库关系**

- Employee 表与 Attendance 表关系：

  - 一对多关系，一个员工可以有多条考勤记录。
- Employee 表与 SalaryRecord 表关系：

  - 一对多关系，一个员工可以有多条工资记录。
- Project 表与 Employee 表关系：

  - 多对多关系，一个项目可以有多个员工，一个员工可以参与多个项目。
- Project 表与 SalaryRecord 表关系：

  - 一对多关系，一个项目可以有多条工资记录。

**4. 数据库索引**

为提高查询效率，考虑在以下字段上创建索引：

- Employee 表：
  - EmployeeID
- Attendance 表：
  - EmployeeID
  - Date
- SalaryRecord 表：
  - EmployeeID
  - Date
- Project 表：
  - ProjectID

## (3)总结

通过用例设计，定义了系统核心用例的基本路径的交互和用例实现的参与类类图。同时，进行了系统的数据库设计

，包括实体关系图、表结构设计、数据库关系和索引设计。这些设计将为系统的具体实现提供指导，并确保系统在运行时能够高效地处理数据和支持核心用例的功能。
