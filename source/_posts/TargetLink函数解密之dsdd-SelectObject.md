---
title: TargetLink函数解密之dsdd-SelectObject
tags:
  - Targetlink
categories:
  - Targetlink
date: 2016-03-26 11:31:42
---

在targetLink的众多API中，个人觉得dsdd SelectObject是极其强大的一个，因为dsdd是链接dd文件和block之间的桥梁（暂且这样来形容）。通过dsdd  SelectObject能够获取到dd中的各种属性，结合[get_tlcg_data](http://beeant0512.github.io/2016/03/15/TargetLink%E5%87%BD%E6%95%B0%E8%A7%A3%E5%AF%86-%E4%B9%8B-get-tlcg-data/),[set_tlcg_data](http://beeant0512.github.io/2016/03/17/TargetLink%E5%87%BD%E6%95%B0%E8%A7%A3%E5%AF%86-%E4%B9%8B-set-tlcg-data/)从而实现修改block的各种属性（Variable,Class,Type,Scaling...)。

#### 函数简介
对于SelectObject，官方是这样解释的
```
Opens a modal dialog with which a DD object can be selected. 
Which object are selectable is specified with keywords. 
This command is for internal use only, and its interface may be subject to future modifications.
```
试译：通过关键字打开一个能够选择特定DD属性的模态框

#### 语法
````
[currentPath,bModified] = dsdd('SelectObject'[,'currentPath',<currentPath>],'entryPath',<entryPath>,<keyword1>,<keyword2>, ... ,<keywordn>);
[currentPath,bModified] = dsdd('SelectObject'[,'currentPath',<currentPath>],'objectKind',<objectKind>,<keyword1>,<keyword2>, ... ,<keywordn>); 
````

#### 输入参数说明
|Name |Type  |Description
|:----|:----|:----|
|currentPath |string |current value for reference property
|objectKind |object kind |string or cell array of strings specifies object kind(s)
|entryPath |DD path |relative DD root where objects reside

#### 输出参数说明
|Name|Type|Description 
|:----|:----|:----|
|currentPath| string| object which has been selected (empty string if no object hase been selected)
|bModified| boolean| 1 if user has selected an object, 0 if not
#### 举例
打开数据类型模态框，设置仅显示整型，且默认值Int8为选中
```
>> selectedType = dsdd('SelectObject','CurrentPath','Int8','objectKind','Typedef','OnlyInteger')

selectedType =

UInt16
```
<img src="/images/targetlink/selectObject/01.png"  alt="打开" /> <img  src="/images/targetlink/selectObject/02.png" alt="选中" />

#### ObjectKind列表
|objectKind| 试译 |
|:-------|:-------|
|AccessFunction |Describes a function that provides access to a variable in the production code. |
|AccessFunctionTemplate |Template for access functions. |
|Acknowledgement |Describes the acknowledge behavior of a sender-receiver data element. |
|Action |Specifies an action that should be started when a message is received or an alarm expires. |
|Alarm |Describes an OSEK OS alarm. |
|Annotation |Enables to add annotations to the object that owns an instance of this object. |
|ApplicationDataTypeComponent |Defines one structure component of a data type on the application level. |
|ApplicationDataTypeGroup |Used to group ApplicationDataType objects. |
|ApplicationDataType |Defines a data type on the application level. |
|ApplicationError |Describes a user-defined error that is associated with an element of an interface. |
|ApplicationMode |Defines properties of a OSEK application mode. |
|Application |Describes an application built from code generated for one or more Simulink systems. |
|AsynchronousServerCallPoint |Describes an AUTOSAR asynchronous server call point. |
|AsynchronousServerCallResultPoint |Describes an AUTOSAR asynchronous server call result point. |
|AutosarAccessPoint |Describes an AUTOSAR access point. |
|Autosar |This object keeps AUTOSAR-related objects. |
|BaseTypes |Specifies base datatypes that are used. Each child object describes one particular base data type. |
|BlockGroup |Used to group Block objects. BlockGroup objects correspond with subsystem blocks in Simulink models, or with Simulink models. |
|Block |Describes a Simulink block. In the Subsystems area, Block objects describe blocks in the Simulink system that has been processed by the Code Generator. In the Pool area, Block objects can be used for DD based code generation. |
|BlockVariable |Describes a Simulink block variable. |
|Build |Describes an executable that was built to run the production code application. |
|CalPrmAccessPoint |Describes an AUTOSAR access point for a calibratable parameter. |
|CalPrmComSpec |Defines how a calprm element is accessed by the receiver. |
|CalPrmElement |Describes a calibration parameter in a CalPrmInterface. Calibration parameters are typically declared as constants (read-only) in the source code. Nevertheless, such parameters may be modified by a calibration system. |
|CalPrmInterface |Defines an interface which contains calibratable parameters. The interface is provided by a CalPrm component and consumed by one or more application components. |
|CalibrationMethod |Defines a calibration method that can be used to access the target hardware, for example, InCircuit, SERAM, DSERAP, BSERAP. |
|CatalogEntry |Object representing a file reference with additional information. |
|CatalogGroup |Used to group calatog objects. |
|Catalog |Contains file references and file category information of files such as source code files (.h/.c) or AUTOSAR files (.arxml/.epc). |
|ClientComSpec |Describes communication attributes for an operation call (client side). |
|ClientPort |Describes an AUTOSAR require client-server port. |
|ClientServerInterface |Defines an interface which contains operations that a client may invoke on a server. |
|CodeGenerationUnitGroup |Used to group CodeGenerationUnit objects. |
|CodeGenerationUnit |Used to specify code generation form DDs. |
|Config |The Config object contains general configuration data. Each DD has one Config object which is a child of the DD's root. |
|Container |Contains additional data attached to a DD object. |
|Counter |Describes a counter that is used by the operating system. |
|CoverageData |Contains data for code coverage analysis. |
|CustomCodeFile |Describes the content of a custom code file as used by TargetLink Custom Code blocks. |
|CustomCodeSection |Describes one custom code section. |
|DDIncludeFile |Specifies a DD file which is automatically loaded (saved) when a DD project is opened (closed). DDIncludeFile objects are thus used to specify points of inclusion. |
|DDUseCase |Defines a use case for the Data Dictionary Manager. |
|DDUseCaseView |Specifies a view for a given object kind in a DD use case, i.e. which child objects are visible. |
|DataDict |Root element of a Data Dictionary workspace. There is only one DataDict object in each DD. |
|DataElement |Describes a data element, for example, a member of a sender/receiver interface. |
|DataFilter |Defines a filter which can be applied to a received data elements, for example, to exclude values which are out of range. |
|DataReadAccess |Describes an AUTOSAR data read access. |
|DataReceivePoint |Describes an AUTOSAR data receive point. |
|DataReceiverComSpec |Defines how a data element is accessed by the receiver. |
|DataSendPoint |Describes an AUTOSAR data send point. |
|DataSenderComSpec |Defines how a data element is accessed by the sender . |
|DataTypeMap |Specifies a mapping between an ApplicationDataType object and a Typedef object. |
|DataTypeMappingSetGroup |Used to group DataTypeMappingSet objects. |
|DataTypeMappingSet |Represents a list of mappings between ApplicationDataType and Typedef objects, as well as a list of mappings between ModeDeclarationGroup and Typedef objects. |
|DataVariantItem |Specifies one data variant item. The DataVariant's DataVariantItem child objects with their variant IDs constitute one data variant. |
|DataVariant |Defines a data variant. Data variants can be switched at runtime. |
|DataWriteAccess |Describes an AUTOSAR data write access. |
|DeviceGroup |Used to group Device objects. |
|Device |Describes a device in the model. |
|DynamicComponent |Defines a component of a struct or union. |
|EMLFunctionGroup |Used to group EMLFunction objects. |
|EMLFunction |Defines properties of an EML function. |
|Event |Describes an operating system event. |
|EventReceiverComSpec |Defines how an event data element is accessed by the receiver. |
|EventSenderComSpec |Defines how an event data element is sent . |
|ExchangeableWidth |Defines a set of variable widths used for width invariant code generation. |
|ExclusiveArea |Defines an exclusive area, that means a part of the code which is protected against interrupts. The actual type of protection mechanism is selected when performing the mapping onto the RTOS. . |
|Experiment |Specifies experiment configurations. |
|FileInfo |Specifies how a file should be generated. |
|FileSpecification |Describes attributes of files which are needed to build an application, for example, generated code files, legacy code files, etc. . |
|FunctionClassGroup |Used to group FunctionClass objects. |
|FunctionClass |Defines C attributes of a function in production code. |
|FunctionClassTemplate |FunctionClassTemplate objects specify which FunctionClass object should be used when no FunctionClass object is specified. Filter rules define when the FunctionClasstemplate object applies. |
|FunctionGroup |Used to group Function objects. |
|FunctionInstance |Describes one instance of a function. |
|Function |In the Pool area, Function objects describe how functions in the production code should be generated. In the Subsystems area, Function objects describe functions that were generated by the Code Generator. |
|FunctionTemplate |FunctionTemplate objects describe rules how functions that match a specified filter conditions should be generated. |
|Generic |Generic objects are used to specify arbitrary data that are not defined by the Data Model. |
|IFDataBlob |Specifies ASAP2 specific blob data information. |
|IFData |Specifies ASAP1b specific IF_DATA information (A2L_BLOB). The name contains the value of the name1 struct element which is usually 'IF_DATA'. |
|IFDataSourceBlob |Describes an ASAM-MCD 2MC source blob. |
|IFDataTokenList |Contains an ASAM MCD 2MC (ASAP2) specific list of tokens (from A2L_TOKEN_LIST). |
|ISR |Describes an interrupt service routine. |
|IncludedCodeFile |Specifies header files which are included to a module. |
|InterRunnableVariableReadAccess |Describes an AUTOSAR inter runnable data read access. |
|InterRunnableVariableWriteAccess |Describes an AUTOSAR inter runnable data write access. |
|InterfaceGroup |Used to group Interface objects. |
|InterfaceVariable |Describes a variable which belongs to a function interface. The variable can be a global input or output, a formal or actual argument, or the function's return value. |
|LogVariableGroup |Used to group LogVariable objects. |
|LogVariable |Describes a variable to be logged during simulations. |
|LookupFunctionTemplate |LookupFunctionTemplate objects describe rules how look-up functions that match a specified filter conditions should be generated. |
|MemorySegment |Defines properties of an address range in target memory. |
|MessageAccessor |Specifies how a message variable is accessed by the sender or the receiver. |
|Message |Describes a communication connection. In the Pool area, Message objects specify how communication connections should be generated. In the Subsystems area, Message object describe how communication connections have been implemented by the Code Generator. |
|MessageVariable |Defines a variable used to hold message data. |
|ModeAccessPoint |Describes an AUTOSAR mode access point. |
|ModeDeclarationGroupGroup |Used to group ModeDeclarationGroup objects. |
|ModeDeclarationGroup |Defines a group of modes, which exist for a given application mode of the ECU, for example, INIT, RUN, TERMINATE, ... |
|ModeDeclaration |Defines an available ECU mode, for example, INIT. |
|ModeDisablingDependency |Specifies a mode that disables the RTE event this object belongs to. |
|ModeElement |Describes an element of a sender/receiver interface which is used to communicate ECU modes (Init, .., Term) to a software component. In AUTOSAR, mode elements are called 'ModeDeclarationGroupPrototypes'. |
|ModeReceiverComSpec |Describes attributes for receiver communication. |
|ModeReceiverPort |Describes an AUTOSAR mode receiver port. |
|ModeRequestTypeMap |Specifies a mapping between a ModeDeclarationGroup object and a Typedef object. |
|ModeSenderComSpec |Describes attributes for sender communication. |
|ModeSenderPort |Describes an AUTOSAR mode sender port. |
|ModeSwitchInterface |Describes an AUTOSAR mode switch interface. |
|ModeSwitchPoint |Describes an AUTOSAR mode switch point. |
|ModelGroup |Used to group Model objects. |
|Model |Describes a Simulink model. |
|ModuleGroup |Used to group Module objects. |
|Module |Secifies a module in production code. |
|ModuleOwnerShipGroup |Used to group ModuleOwnerShip objects. |
|ModuleOwnerShip |Specifies module ownership. |
|ModuleTemplate |Template for code modules. |
|OILEntry |Describes one entry in a OIL file. |
|OILFile |Contains the memory image of a complete OIL file. |
|OperationArgument |Describes an argument of a operation. Operations are elements of client/server interfaces, that means functions which a client component may invoke on a server component. |
|Operation |Describes an operation. Operations are elements of client/server interfaces, that means functions which a client component may invoke on a server component. |
|PageSwitchingInfo |Describes a code page which can be switched. |
|PerInstanceMemoryVariableAccess |Describes an AUTOSAR per instance memory variable access. |
|Pool |The Pool object is a child of the DD root and constitutes the Pool area in which data for code generation are specified. |
|PortGroup |Used to group AUTOSAR port objects. |
|Port |Describes a port of a Simulink system. |
|PropertyValueList |List of propertyname/value pairs. All property values are strings. Additional PropertyValueList objects can be inserted to create a hierarchical composition. |
|ProtectionMechanism |Defines a mechanism used to protect code sections against preemption by tasks or ISRs. |
|ProvideCalPrmPort |Describes an AUTOSAR SWC port where a CalPrmInterface is provided. |
|RTOS |Contains RTOS objects needed for multirate code generation. |
|Raster |Defines a measurement raster which can be used for data acquisition by a calibration system. |
|ReceiverPort |Describes an AUTOSAR require sender-receiver port. |
|RecordLayout |Specifies how a table map for a look-up function should be generated. |
|RequireCalPrmPort |Describes an AUTOSAR SWC port where a CalPrmInterface is required. |
|RequirementInfo |RequirementInfo objects keep Simulink RMI data. |
|Resource |Describes an OSEK OS resource. |
|RootFunctionTemplate |Template for root functions (STEP, INIT, RESTART, TERM, ...). |
|RteEvent |Describes an RTE event. |
|Runnable |Describes an AUTOSAR runnable. |
|ScalingGroup |Used to group Scaling objects. |
|Scaling |Specifies scaling parameters. |
|Section |Describes a linker section. |
|SenderPort |Describes an AUTOSAR provide sender-receiver port. |
|SenderReceiverInterface |Defines an interface for sending and receiving data via ports. |
|ServerComSpec |Describes communication attributes for an operation call (server side). |
|ServerPort |Describes an AUTOSAR provide client-server port. |
|SharedCalPrmVariableAccess |Describes an AUTOSAR inter runnable shared calibratable access. |
|SoftwareComponentGroup |Used to group SoftwareComponent objects. |
|SoftwareComponent |Describes an AUTOSAR software component including it's internal behavior. |
|StateflowNode |Describes a state or subchart in a Statechart. |
|StructTemplate |Template for structs. |
|SubStructTemplate |Template for substructs. |
|Subfunction |Describes a subfunction called from a function instance. |
|SubsystemConfig |Contains configuration data for a subsystem. This information is evaluated by the Code Generator. |
|Subsystem |Object containing the description of a generated or imported subsystem. |
|SwRecordLayoutContent |This element is used together with SwRecordLayoutElements. It describes the serialization of the data (e.g. a look-up table axis) in the ECU memory. |
|SwRecordLayoutElement |Defines an element (group) in a record layout that describes the serialization of the data (e.g. a look-up table axis) in the ECU memory. |
|SwRecordLayoutGroup |Used to group SwRecordLayout objects. |
|SwRecordLayout |Used to describe the various record layouts of the calibratable object (especially look-up table data) in the memory of the ECU. |
|SymbolGroup |Used to group Symbol objects. |
|Symbol |Defines object kind symbol. |
|SynchronousServerCallPoint |Describes an AUTOSAR synchronous server call point. |
|Task |Describes a operating system task. |
|TaskTemplate |Defines properties of a task which are not explicitly defined in the model. |
|TemplateGroup |Used to group template objects. |
|TypedefComponent |Defines a component of a struct or union data type. |
|TypedefEnumValue |Defines an element of an enum union data type. |
|TypedefGroup |Used to group Typedef objects. |
|Typedef |Specifies a data type. In the Pool area, Typedef objects serve as templates that describe how a data type should be generated. In the Subsystems area, Typedef objects describe how a data type was generated in the production code. |
|TypedefTemplate |Specifies attributes of struct, enum, or union data types that are generated implicitly. |
|Unit |Defines a physical unit based on SI units. |
|VariableClassGroup |Used to group VariableClass objects. |
|VariableClass |Defines C attributes of variables in the production code. |
|VariableClassTemplate |VariableClassTemplate objects specify which VariableClass object should be used when no VariableClass object is specified. Filter rules define when the VariableClasstemplate object applies. |
|VariableGroup |Used to group Variable objects. |
|Variable |Variable objects describe variables in production code. In the Pool area, Variable objects serve as templates that specify how a variable should be generated. By associating a TargetLink block variable (for example, a block's output) with a Variable object in the Pool area, the properties of the Variable object determine how the block variable should be represented in production code. In the Subsystems area, Variable objects describe how an instance of a variable was generated in production code. |
|VariableTemplate |VariableTemplate objects specify how implicit variables should be generated in the production  code. |
|VariantConfig |Defines a variant configuration. This variant configuration is activated by setting the /Config/ TargetLink.ActiveVariantConfig property to the name of this object. |
|VariantItem |Defines a variant. VariantItem objects enable to associate varianted properties with variant configurations described by VariantConfig objects. |
|WaitPoint |Describes an AUTOSAR wait point. |
