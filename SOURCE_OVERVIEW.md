## Обзор папки `Source` Model Studio CS

Этот файл описывает **все верхнеуровневые папки** в `D:\WORK\SAP\Model Studio\Source` и их назначение.  
Для каждой папки дано краткое объяснение по смыслу модуля, чтобы понимать, **за что он отвечает** и как ориентироваться в исходниках.

> Внутри каждой из этих папок находятся свои подпроекты (`.vcxproj`, `.csproj`, `.cpp/.h` и т.п.).  
> Если нужно, отдельные модули можно разобрать подробнее (до уровня файлов) в отдельных документах.

---

### 1. Инфраструктура и общее ядро

- **`Source/Common`**  
  Общие библиотеки, вспомогательные классы и утилиты, которые используются разными подсистемами.

- **`Source/CommonResource`**  
  Общие ресурсы: иконки, строки, меню, шаблоны и прочие UI‑ресурсы для разных модулей.

- **`Source/Settings`**  
  Глобальные настройки системы: конфигурационные файлы, профили, опции работы модулей.

- **`Source/Params`**  
  Определения типов параметров, их настроек, возможно — справочники параметров и связанных данных.

- **`Source/msData`**  
  Реализация ядра работы с данными/параметрами (соответствует интерфейсам `MStudioData` из `CSDataInterfaces.h`).

- **`Source/mstudioDB`**, **`Source/mstudioDbCache`**, **`Source/mstudioDBReports`**  
  Ядро базы данных Model Studio, кэширование данных и отчёты по БД (спецификации, ведомости и т.п.).

- **`Source/mstudioUI`**, **`Source/mstudioFrame`**  
  Элементы пользовательского интерфейса, главное окно/фрейм приложения, панели, диалоги и т.д.

- **`Source/mstudioReports`**  
  Механизмы формирования отчётов/ведомостей (таблицы, спецификации, формуляры).

- **`Source/mstudioCalc`**  
  Общие расчётные модули (базовая логика для специализированных расчётов).

- **`Source/msEnvironment`**, **`Source/msEnvironmentObjects`**  
  Окружение проекта: объекты среды, площадки, возможно — подложки/фоновые данные.

- **`Source/ProductVersion`**  
  Данные о версии продукта, компоненты для отображения/проверки версий, возможно, автообновление.

- **`Source/lib`**, **`Source/packages`**  
  Внешние и внутренние библиотеки/пакеты, на которые зависят проекты (сторонние компоненты, общие модули).

- **`Source/Support`**  
  Конфигурационные файлы, меню, описания команд (например, `ms_pipe.cfg`, `water.cfg` и др.).

---

### 2. Обвязка AutoCAD/NCAD, загрузчики и enabler

#### 2.1. `Source/Enabler`

- **`Resource.h`** – идентификаторы ресурсов (диалоги, строки, иконки) enabler‑модуля.  
- **`StdAfx.h`** – предкомпилируемый заголовок (подключает MFC/ARX и общие заголовки для этого проекта).

Enabler‑модуль обеспечивает загрузку и корректное отображение объектов Model Studio в AutoCAD/NCAD.

#### 2.2. `Source/linCSLoader`

- **`AboutDlg.h`** – диалог “О программе” для модуля загрузчика.  
- **`DocData.h`** – структура/класс данных документа (состояние модуля на документ).  
- **`HcStrings.h`** – строковые константы/идентификаторы (human‑readable strings).  
- **`lcsLoaderDocManagerReactor.h`** – реактор менеджера документов AutoCAD (открытие/закрытие чертежей).  
- **`lcsLoaderEditorReactor.h`** – реактор редактора AutoCAD (события в редакторе, загрузка/инициализация).  
- **`Resource.h`** – ресурсы (диалоги, строки, иконки) загрузчика.  
- **`SplashWnd.h`** – окно заставки (splash) при загрузке.  
- **`StartupDlg.h`** – стартовый диалог/мастер при запуске модуля.  
- **`StdAfx.h`** – предкомпилируемый заголовок проекта.

Этот модуль управляет инициализацией LinCS/Model Studio при старте AutoCAD/NCAD.

#### 2.3. `Source/LinCSObjects`

- **`HcStrings.h`** – строки/идентификаторы для LinCS‑объектов.  
- **`linCSGroundData.h`** – данные о “земле”/основании для объектов LinCS.  
- **`linCSLink.h`** – класс связи (link) в модели (связи между узлами).  
- **`linCSLinkBehaviours.h`**, **`linCSLinkCloneBehavioursImpl.h`** – поведение связей и логика клонирования.  
- **`linCSModelSettingsEx.h`**, **`LinCSObjSettings.h`**, **`LinCSSettings.h`** – настройки модели/объектов LinCS.  
- **`linCSNodeEx.h`** – расширенный узел (node) сети.  
- **`linCSNodeLinkAssociation.h`** – ассоциации узлов и связей.  
- **`linCSUnitEx.h`** – расширенный “юнит”/элемент LinCS.  
- **`linGarland.h`** – объекты/модель гирлянд (подвешенные провода/кабели).  
- **`Resource.h`** – ресурсы модуля.  
- **`StdAfx.h`** – предкомпилируемый заголовок.

Папка содержит основные ARX/DBX‑классы, представляющие объекты LinCS в чертеже.

#### 2.4. `Source/linCSCom`

- **`CSlink.h`** – COM‑обёртка для связей (link).  
- **`CSLinkPropWrapper.h`** – обёртка для свойств связи (доступ из COM).  
- **`dlldatax.h`** – служебный файл для регистрации COM‑библиотеки (DLL data).  
- **`linCSCom.idl`** – IDL‑описание COM‑интерфейсов линейных объектов (генерация `.tlb`/обёрток).  
- **`MDSELLinkMode.h`** – режимы/способы выбора связей.  
- **`Node.h`** – COM‑обёртка для узла (node).  
- **`resource.h`** – ресурсы (ID).  
- **`stdafx.h`** – предкомпилируемый заголовок.  
- **`VS16/.../linCSCom.h`** – сгенерированные заголовки для разных конфигураций (FullDebug/Release, NCAD версий).

Этот модуль предоставляет COM‑доступ к объектам LinCS (узлы, связи, их свойства).

#### 2.5. `Source/LinCS3d`

Большой набор заголовков, реализующих 3D‑ядро LinCS и его UI:

- Диалоги/интерфейс: `CalcGD_dialog.h`, `CalcGD_help.h`, `CDialogCGD.h`, `CDialogHelpCGD.h`, `CDialogProperties.h`, `ELAYGarlandWizardDlg.h` и др.  
- Геометрия и данные: `eline.h`, `InfoCGD.h`, `IntegrityChecker.h`, `LibAssemblyData.h`, `StructuresCGD.h`, `NetworkDataExport.h`.  
- Реакторы AutoCAD: `lcsDbReactor.h`, `lcsDocManagerReactor.h`, `lcsEditorReactor.h`, `lcsEntityReactor.h`.  
- Настройки/утилиты: `LinCSAppSettings.h`, `LCSUtil.h`, `MessagesCGD.h`, `SchemaGroupsCGD.h`, `SchemaParameterCGD.h`, `SchemaPropertiesCGD.h`, `SchemaTablesCGD.h`.  
- Вспомогательные классы UI: `CPropertyCGD.h`, `CPropertyFormulaCGD.h`, `CPropertyGridCGD.h`, `CPropertyGroupCGD.h`, `CSplitterCGD.h`, `CTollbarCGD.h`, `CWidgetCGD.h`, `CListCGD.h`.  
- Интеграция: `urs4AdtExports.h`, `WireConnectorInterface.h`.  
- Служебные: `DocData.h`, `HcStrings.h`, `resource.h`, `StdAfx.h`.

Здесь реализуется 3D‑геометрия и пользовательский интерфейс для LinCS.

#### 2.6. `Source/UnitsCS`

Основное ядро UnitsCS:

- **Интерфейсы и реализация ядра**:  
  - `CSModelStudioCoreInterfaces.h`, `CSModelStudioCoreInterfacesImpl.h` – интерфейс `IMStudioCore` и его реализация.  
  - `CSParametricInterfaces.h`, `CSParametricInterfacesImpl.h`, `CSParametricConstants.h` – параметрическое ядро и константы.

- **Общие типы и утилиты**:  
  - `BoundingVolume.h`, `msGDIPlusObjects.h`, `msPointCollision.h`, `msTextBox.h`, `MSElementStream.h`, `ucsCommon.h`, `UnitCSTools.h`.

- **Объекты и ассоциации LinCS/UnitsCS**:  
  - `linCSDataObject.h`, `linCSDwgData.h`, `msObjectAssociation.h`.  
  - `linCSBlockRefEx.h`, `linCSBlockRefExViews.h`, `linCSCOWBlockRef.h` – расширенные блок‑ссылки.  
  - `linCSBoundaryBox.h`, `linCSCentroidMarker.h`, `linCSCollision.h`, `msPointCollision.h`.  
  - `linCSNode.h`, `linCSNodeLinkAssociationBase.h`, `linCSLinkBase.h`, `linCSLinkAssociationNode.h`.  
  - `linCSModelSettings.h`, `LinCSSettings.h`.

- **Параметрические объекты**:  
  - `linCSParametricEnt*.h` (несколько вариантов: `Base`, `Base2`, `Ent2`, `EntExViews`, `Jig` и др.).  
  - `linCSUnitsGripAppData.h`, `linCSParametricEntJig.h` – работа с грипами/джигами.

- **Прочее**:  
  - `linCSInsulationDesignation*.h` – обозначения изоляции.  
  - `linCSLimitationZone.h` – зоны ограничений.  
  - `linCSMarker.h`, `linCSText.h`, `linCSViewportDef.h`, `linCSViewportFrame.h`, `linCSWorkSpace.h`.  
  - `mstGrounding*.h` – заземление и его объекты.  
  - `HcStrings.h`, `NodeModes.h`, `nodesCallBacks.h`, `Resource.h`, `SectionNodesDlg.h`, `StdAfx.h`, `ursPETemplates.h`.

#### 2.7. `Source/UnitsCSCom`

COM‑обёртки для UnitsCS:

- **Базовые COM‑типы**:  
  - `_IMDSUnitsFactoryEvents_CP.h` – шаблон событий COM‑фабрики.  
  - `EnumVariant.h`, `ItemCollection.h` – перечислители/коллекции.

- **Основные COM‑обёртки**:  
  - `MDSUnitsFactory.h` – фабрика COM‑объектов UnitsCS.  
  - `MDSObjects.h`, `MDSNodes.h`, `MDSGrounding.h`, `MDSViewportFrame.h`, `MDSBoundaryBox.h`, `MDSFileDlgWrapper.h`.  
  - `Element.h`, `Elements.h` – элементы модели.  
  - `Parameter.h`, `Parameters.h` – параметры и наборы параметров.

- **Диалоги/шаблоны**:  
  - `DiaWrapParametric.h`, `TmplCommonProp.h`.

- **Обёртки над конкретными объектами**:  
  - `WrBlockRefEx.h`, `WrCOWBlockRef.h`, `WrCSInsulationDesignation.h`, `WrDataObject.h`, `WrGroupDia.h`, `WrMaterialDia.h`, `WrMaterialStandardDia.h`, `WrNode.h`, `WrParametricEnt.h`, `WrTypeDia.h`, `WrViewportDef.h`, `WrWorkSpace.h`.

- **Служебные**:  
  - `UnitsCSCom.idl` – IDL‑описание COM‑интерфейсов.  
  - `HcStrings.h`, `resource.h`, `StdAfx.h`.  
  - `VS16/.../UnitsCSCom.h` – сгенерированные заголовки для разных конфигураций.

#### 2.8. `Source/CSGraphics`

Низкоуровневая 2D/3D‑геометрия и графика:

- **Базовые геометрические сущности**:  
  - Точки/векторы: `Vector3.h`, `CSLine3.h`, `CSSegment2D.h`, `CSSegment3d.h`.  
  - Плоскости и объёмы: `CSPlane3.h`, `CSBox.h`, `CSExtents.h`.  
  - Кривые/контуры: `CSCurve3d.h`, `CSContour.h`, `CSContourElement.h`, `CSEntity2D.h`, `CSEntity3D.h`.  
  - Меши: `CSMesh.h`, `CSPackedMesh.h`, `CSMeshPreprocess.h`, `CSMeshSimplification.h`.

- **Тела вращения и поверхности**:  
  - `CSCylinder.h`, `CSCylSlope.h`, `CSCylSlopeIntersect.h`, `CSSphere.h`, `CSTorus.h`, `CSTorusArc.h`, `CSDish.h`, `CSCone.h`, `CSConeEx.h`, `CSDisc.h`, `CSWedge.h`, `CSPyramid.h`, `CSRevolve.h`.  
  - Профили: `CSProfileElt.h`.

- **Структуры пространственных данных**:  
  - `CSOcTree.h`, `CSQuadTree*.h`, `CSPointRTree.h`.

- **Текст и триангуляция**:  
  - `CSText.h`, `CSTextBox.h`.  
  - Папки `triangl` и `triangulate_text` – реализация триангуляции (poly2tri и своя геометрия).  
  - `TriTriIntersect*.h`, `triangle_distance*.h`.

- **Интерфейсы графики**:  
  - `CSGraphics.h`, `CSGraphicsInterfaces.h`, `CSGraphicsInterfacesImpl.h`, `CSGraphicsCache*.h`, `CSGroup.h`, `CSArrayCirc.h`, `CSArrayRect.h`, `CSBooleanGroup.h`, `CSBooleanProcessor.h`, `CSMatrix.h`, `CSTriangulate.h`.

- **Служебные файлы**:  
  - `ms3DTypes.h` (типы для 3D), `CSpredicates.h`, `Resource.h`, `stdafx.h`, `targetver.h`.

#### 2.9. `Source/CSGraphicsArx`

ARX‑обвязка для CSGraphics и интеграция с AutoCAD:

- **Обёртки и конвертеры**:  
  - `Conversion.h` – конвертация типов между AutoCAD и CSGraphics.  
  - `CSBrepExtractor.h` – извлечение BREP‑геометрии из объектов AutoCAD.  
  - `CSCurveWraper.h` – обёртка над кривыми.  
  - `CSExtendedWorldDraw.h` – расширенный вывод (WorldDraw) для AutoCAD.  
  - `CSMeshCache.h`, `CSMeshDumper.h` – кэш и дамп мешей.  
  - `CSObjectsMinDistance.h` – вычисление минимальных расстояний.  
  - `CSPackedMesh.h` – работа с упакованным мешем в контексте ARX.  
  - `CSTextTriangulator.h`, `CSTriangulator.h` – триангуляция текста и объектов.

- **DirectX‑заголовки**:  
  - `d3d9*.h`, `d3dx9*.h` – SDK DirectX, используемый для визуализации.

- **Инфраструктура**:  
  - `DocData.h`, `DrawWrapper.h`, `nweGeneration.h`, `Resource.h`, `stdafx.h`.  
  - Папка `triangl` – копия/общая часть триангулятора (как в `CSGraphics`).

#### 2.10. `Source/CSGraphicsTests`

Тестовые заголовки для проверки CSGraphics:

- **`CCSBoxTest.h`** – тесты для `CSBox`.  
- **`CSVECTORD2Test.h`** – тесты для двумерных векторов/типов.  
- **`stdafx.h`**, **`targetver.h`** – служебные заголовки проекта тестов.

#### 2.11. `Source/ViperCS`

Главный модуль Viper (команды, UI, диалоги):

- **Реакторы и интеграция**:  
  - `AVM_DBReactor.h`, `AVM_EntityReactor.h` – реакторы БД и сущностей.  
  - `vCSDbReactor.h`, `vCSEditorReactor.h`, `vCSInputContextReactor.h`, `vCSTransactionReactor.h`, `vCSUpdateFormProjectReactor.h`.

- **Создание труб/объектов**:  
  - `vCSCreatePipe.h`, `vCSCreateViper.h`, `CreateBuildStruct.h`, `CTracelineCreator.h`, `CVCSTracerCallback.h`.  
  - `vCSParallelPipe.h`, `vCSPipeCopy.h`, `vCSPipeWeldCreator.h`, `VCSUtils.h`, `vCSViperFactory.h`, `vCSViperLibraryFactory.h`.

- **Диалоги и UI**:  
  - `ImportDlg.h`, `InsulationExportDlg.h`, `PipeInsulationPane.h`, `PipeLibSplitWnd.h`, `PrototypeSelectDlg.h`, `ParallelPipesDialog.h`, `StopValvesInserter.h`, `ValveAssemblyWizard.h`, `VAxoGenerator.h`, `PipeConnectorInterface.h`.  
  - `vCSDlg_*` (несколько диалогов: выбор DN, изменение уклона, комбобоксы и т.п.).  
  - `vCSGraph*.h`, `vCSGrillJig.h`, `vCSHoleCreator.h`, `vCSTracingPaletteSet.h`, `vCSViperPanes.h`, `PipeProps.h`.

- **Экспорт/импорт**:  
  - `SCPipeExport.h`, `ExportInsulation.h`, `InsulationExportDlg.h`, `VAxoGenerator.h`, `vCSExport.h`, `vCSRapidJson.h`.

- **Jig/интерактив**:  
  - `MSTracerJig.h`, `vCSFlexSegmentJig.h`, `vCSObjectJig.h`, `vCSPointMonitor.h`, `vCSViewportAutoProfile.h`, `vCSUserInputHelper.h`.

- **Служебные**:  
  - `AXOGen.h`, `COlePicture.h`, `DocData.h`, `HcStrings.h`, `Resource.h`, `StdAfx.h`.

#### 2.12. `Source/ViperCSObj`

Объектная модель Viper (геометрия, логика трасс и арматуры):

- **Базовые классы и исключения**:  
  - `AVM_Core.h`, `AVM_Interface.h`, `AVM_Object.h`, `vCS_DM_Base.h`, `vCS_DM_Exception.h`, `vCS_Exception.h`.

- **Data‑model (DM) для трассы**:  
  - `vCS_DM_Axis*.h`, `vCS_DM_Node*.h`, `vCS_DM_Branch.h`, `vCS_DM_Seg.h`, `vCS_DM_SubSeg.h`, `vCS_DM_Support.h`, `vCS_DM_Weld.h`, `vCS_DM_InLine.h`, `vCS_DM_ILBase.h` и др.  
  - Это логическая модель: оси, узлы, сегменты, опоры, сварки, inline‑элементы.

- **Геометрия и структура**:  
  - `vCSAxis.h`, `vCSBranch.h`, `vCSDataStructures.h`, `vCSDimStructures.h`, `vCSDivider.h`, `vCSLayers.h`, `vCSMinidirStructures.h`, `vCSTypes.h`.  
  - `vCSSegment.h`, `vCSSubSegment.h`, `vCSOverpassAxis.h`.

- **Создание/модификация труб**:  
  - `vCSCreateBypass.h`, `vCSCreateNewEntOnSeg.h`, `vCSCreateUShaped.h`, `vCSCreateVerticalSection.h`.  
  - `vCSPipeCopy.h`, `vCSPipeMove.h`, `vCSPipeRotate.h`.  
  - `vCSInLine.h`, `vCSInLOffset.h`, `vCSNonPassableDuct.h`.

- **Арматура, узлы и соединения**:  
  - `vCSNode*.h` (Node, NodeBase, NodeConnector, NodeElbow, NodeTerminator, и др.).  
  - `vCSConnect*.h`, `vCSC_Elb_Elb*.h`, `vCSCon_Common.h` – разные типы соединений.  
  - `vCSSupport.h`, `vCSWeld.h`, `vCSWeldConnectionDlg.h`.  
  - `vCSGrillObject.h`, `VentParamsNarrowingDlg.h`.

- **Параметрические профили и инструменты**:  
  - `vCSProfileBase.h`, `vCSProfileCircle.h`, `vCSProfileRect.h`.  
  - `vCSSettings*.h` (экспорт в PCF/Axogen/Start, tracing‑настройки).  
  - `vCSTools*.h` (общие, геометрические, строковые, выбор и др.).  
  - `vCSJig*.h` (InLine, Support, структуры Jig и др.).  

- **Экспорт/интеграция**:  
  - `vCSExport2PCF.h`, `vCSExportToAxogen.h`, `vCSExportToStart.h`.  
  - `vCSAssyDwgFiler.h`, `vCSWorldDraw.h`, `vCSSubEntityTraits.h`.

- **Прочие**:  
  - `AngleListDlg.h`, `CGSPipeProfile.h`, `InsulationUtils.h`, `MultiPipeInsulation.h`, `PipeTracingParamsDlg.h`, `MSTracerBox.h`.  
  - `HcStrings.h`, `resource.h`, `StdAfx.h`, `vCSInterfaces.h`, `vCSUCS.h`, `VCSEntityExtInterface.h`, `vCSObject.h`, `vCSEntity.h`, `vCSDrawable*.h`.

#### 2.13. `Source/ViperCSObjCom`

COM‑обёртки для объектов Viper:

- **Базовые и служебные**:  
  - `HcStrings.h`, `resource.h`, `StdAfx.h`.  
  - `ViperCSObjCom.idl` – IDL‑описание COM‑интерфейсов.  
  - `TmplCommonProp2.h`, `vCSTmplCommonProp.h` – шаблоны общих свойств.  
  - `VS16/.../ViperCSObjCom.h` – сгенерированные заголовки.

- **Wr‑обёртки**:  
  - `WrAxis.h`, `WrCommon.h`, `WrDiameter*.h`, `WrDivider.h`, `WrEntity.h`, `WrInLine.h`, `WrInsulation.h`, `WrMpInsul.h`, `WrNode*.h`, `WrOverpassAxis.h`, `WrPropDia.h`, `WrSegment.h`, `WrSubSegment.h`, `WrSupport.h`, `WrTools.h`, `WrWeld.h`.

#### 2.14. `Source/ViperCSObjPatch`

- **`DocData.h`** – данные документа для патча.  
- **`Resource.h`** – ресурсы модуля.  
- **`StdAfx.h`** – предкомпилируемый заголовок.  
- **`vCSPatchImpl.h`** – реализация патчей/исправлений для объектов Viper.

#### 2.15. `Source/ViperCSRename`

- **`DocData.h`** – данные документа.  
- **`Resource.h`** – ресурсы.  
- **`StdAfx.h`** – предкомпилируемый заголовок.  
- **`vCSRenamer.h`** – основной класс переименования объектов/элементов.  
- **`vCSRenameSettings.h`**, **`vCSRenameUtils.h`** – настройки и утилиты для операций переименования.

#### 2.16. `Source/ViperCStart`

- **`ImportAppStart.h`**, **`ImportAppStartGetter.h`**, **`ImportAppStartInterf.h`** – интерфейс и реализация запуска импортирующего приложения/подсистемы Viper Start.  
- **`resource.h`** – ресурсы.  
- **`stdafx.h`**, **`targetver.h`** – служебные заголовки проекта.

#### 2.17. `Source/ViperCSTests`

Набор тестов для различных функций Viper:

- **`AcadOutputter.h`** – вывод результатов тестов в AutoCAD.  
- **`CheckEntity.h`**, **`CheckFormatTest.h`**, **`ValidateFormat.h`** – проверки/валидация сущностей и форматов.  
- **`CreatePipeOnPointsTest.h`**, **`ParallelOffsetTest.h`**, **`WorkingWithAxis.h`** – тесты создания трубы по точкам, параллельного смещения, работы с осями.  
- **`ParamsAdapterTest.h`**, **`ParamsGetterTest.h`**, **`ParamsProcessingTest.h`** – тесты работы с параметрами.  
- **`PickTableTest.h`**, **`TableTest.h`** – тесты взаимодействия с таблицами.  
- **`PromptKwordTest.h`**, **`PromptVariantTest.h`** – тесты пользовательского ввода.  
- **`StepAlongPathTest.h`**, **`vCSToolsTests.h`**, **`ViperCS_parallelPipeTests.h`** – тест утилит и параллельных труб.  
- **`StdAfx.h`** – предкомпилируемый заголовок.

#### 2.18. `Source/msLogger`

- **`EventDlg.h`** – диалог отображения/фильтрации событий.  
- **`LoggerWnd.h`** – главное окно логгера.  
- **`Resource.h`** – ресурсы (строки, диалоги).  
- **`stdafx.h`** – предкомпилируемый заголовок.  
- **`Utils.h`** – утилитные функции логгера.

#### 2.19. `Source/msLoggerARX`

- **`DocData.h`** – данные документа для ARX‑модуля логгера.  
- **`loggerpalette.h`** – палитра/панель логгера в AutoCAD.  
- **`msLoggerARX.h`** – основной ARX‑класс/точка входа.  
- **`Resource.h`**, **`StdAfx.h`** – ресурсы и предкомпилируемый заголовок.

#### 2.20. `Source/MSMenuManager`

- **`CMenuManager.h`** – главный класс управления меню и панелями инструментов.  
- **`DocData.h`** – данные документа.  
- **`Resource.h`** – ресурсы (конфиги меню, строки).  
- **`StdAfx.h`** – предкомпилируемый заголовок.

#### 2.21. `Source/ChatLibraryARX`

- **`CHTEnv.h`** – окружение/настройки чат‑библиотеки.  
- **`CSChatPalette.h`** – палитра/панель чата.  
- **`DBChatThreadHost.h`** – хост потоков чата (работа с БД/сообщениями).  
- **`EmoticonHelper.h`**, **`ImageDataObject.h`**, **`ImageHelper.h`, `LibraryImageStore.h`** – работа с картинками и эмодзи.  
- **`MFCToolTipHelper.h`** – подсказки/tooltip’ы.  
- **`RichEditHelper.h`**, **`RtfDefinitions.h`**, **`RtfImageStore.h`** – работа с RichEdit/RTF‑форматом, хранение изображений в RTF.  
- **`resource.h`**, **`stdafx.h`**, **`targetver.h`** – служебные заголовки и ресурсы.


---

### 3. Проекты, структура и иерархии

- **`Source/mstProject`**  
  Основной модуль управления проектами Model Studio (структура проекта, базовые операции).

- **`Source/mstProjectObjects`**, **`Source/mstProjectMessages`**  
  Объекты проекта и система обмена сообщениями/событиями между частями проекта.

- **`Source/mstProjectBuildingHierarchy`**, **`Source/mstProjectStructureHierarchy`**, **`Source/mstProjectCustomHierarchy`**, **`Source/mstStructureDataHierarchyBase`**  
  Иерархия здания (здания/этажи/помещения), структура проекта (разделы/подсистемы), пользовательские иерархии и их базовые классы.

- **`Source/mstProjectCom`**  
  COM‑интерфейсы для работы с проектной структурой из внешних приложений/скриптов.

- **`Source/mstProjectDocuments`**  
  Работа с документами проекта: чертежи, внешние файлы, связи между ними.

- **`Source/mstClpFoldersHierarchy`**  
  Иерархия папок (например, структура библиотек/каталогов в проекте).

---

### 4. Трубопроводы, сети, водоотведение

- **`Source/mstPipeCore`**, **`Source/mstPipeCoreObjects`**  
  Ядро подсистемы трубопроводов (логика трассировки, расчёты, алгоритмы) и объекты трубопроводов.

- **`Source/msPipeNetworks`**, **`Source/msPipeNetworksCom`**, **`Source/msPipeNetworksObjects`**  
  Подсистема трубопроводных сетей: сети, узлы, ветки; COM‑интерфейсы и объекты.

- **`Source/PipePlan`**  
  Плановые представления трубопроводов (чертежи планов труб, схемы планировки).

- **`Source/PipeResource`**  
  Ресурсы для трубопроводной подсистемы: меню, команды, иконки, строки.

- **`Source/PLineResource`**  
  Ресурсы для линий/полилиний, связанных с трассами/сетями.

- **`Source/MSStorm`**,  
  **`Source/MSStormCalcRD`**, **`Source/MSStormCalcRDTR`**, **`Source/MSStormCalcRDTRPlus`**,  
  **`Source/MSStormCalcSO`**, **`Source/MSStormCalcSOPlus`**,  
  **`Source/MSStormCalcSTO`**, **`Source/MSStormCalcSTOPlus`**,  
  **`Source/MSStormCom`**, **`Source/MSStormObjects`**  
  Подсистемы для расчёта и проектирования ливневой/сточной канализации: различные расчётные модули, COM‑слой и объекты.

- **`Source/msTankDesigner`**, **`Source/msTankDesignerObjects`**  
  Проектирование резервуаров/ёмкостей и объекты этих конструкций.

- **`Source/msTDMS`**  
  Модуль TDMS — интеграция или собственная система управления техническими данными.

---

### 5. Кабели, электрика, щиты, схемы

- **`Source/mstCable`**  
  Подсистема кабельных трасс и кабелей (кабельные линии, лотки и пр.).

- **`Source/mstElectrica`**, **`Source/mstElectricaObjects`**  
  Модуль электрики: объекты электротехнических систем (оборудование, линии, сети).

- **`Source/ShieldCS`**, **`Source/ShieldCSCom`**  
  Подсистема щитов (распределительные устройства, щиты управления) и её COM‑слой.

- **`Source/SchematiCS`**, **`Source/SchematiCSCOM`**, **`Source/SchematiCSENT`**, **`Source/ScheMiddle`**, **`Source/SchemaUtils`**  
  Подсистема схем (принципиальные, однолинейные и др.): ядро, сущности, промежуточные слои и утилиты.

- **`Source/SchematicsResource`**  
  Ресурсы для модуля схем: символы, меню, панели инструментов.

- **`Source/CircuitsResource`**, **`Source/CableResource`**, **`Source/PanelResource`**, **`Source/ElayResource`**, **`Source/FactoryResource`**, **`Source/StormResource`**  
  Наборы ресурсов (иконки, строки, меню) для подсистем цепей, кабелей, панелей, электротехнических схем, заводских систем, ливневой канализации.

- **`Source/ElectricalCalc`**, **`Source/ElectricalCalculator`**  
  Электротехнические расчёты: нагрузки, токи, уставки защит и пр.

- **`Source/GarlandMaster`**  
  Подсистема гирлянд (например, провода/тросы на опорах ЛЭП или подвесных систем).

- **`Source/SelectivityMap`**  
  Анализ и визуализация селективности защит (координация работы защитных устройств).

---

### 6. Конструкции, металлоконструкции, геометрия

- **`Source/mstMetal`**, **`Source/mstMetalCOM`**, **`Source/mstMetalObjects`**  
  Подсистема металлоконструкций: объекты металлокаркасов, их COM‑слой и логика.

- **`Source/msAEC`**, **`Source/msAECCom`**, **`Source/msAECObjects`**  
  Архитектурно‑строительные объекты (AEC): стены, перекрытия, проёмы и т.п., и их COM‑интерфейсы.

- **`Source/msGeo`**, **`Source/msGeoCom`**, **`Source/msGeoObjects`**  
  Геодезия и геометрия: поверхности, точки, линии, геодезические объекты, COM‑слой.

- **`Source/mstLandSurfaces`**  
  Модуль работы с поверхностями (земля, рельеф, площадки).

- **`Source/FoundationCalc`**, **`Source/FoundationCalcTest`**  
  Расчёт фундаментов и проекты для тестирования этих расчётов.

---

### 7. Отчёты, публикация, обмен данными

- **`Source/CSPublisher`**  
  Публикация и вывод документов (отчёты, спецификации, ведомости) из модели.

- **`Source/Reporter`**, **`Source/ReporterUnmanaged`**  
  Подсистема отчётов/ведомостей: формирование отчётов, unmanaged‑вариант.

- **`Source/nvExporter`**, **`Source/nvExporterConverter`**, **`Source/nvExporterLoader`**  
  Экспорт в Navisworks/другие форматы, конвертеры и загрузчики для этих форматов.

- **`Source/msAutodocs`**  
  Автоматическое формирование документов (текстовые/табличные отчёты, ведомости, спецификации).

- **`Source/MergePDF`**  
  Объединение и обработка PDF‑файлов (сбор чертежей/отчётов в один документ).

- **`Source/OpenXmlWrap`**  
  Обёртка для работы с OpenXML (Word/Excel) — генерация DOCX/XLSX.

- **`Source/MsToScad`**  
  Экспорт данных из Model Studio в SCAD (расчётное ПО).

- **`Source/pcfXChange`**  
  Обмен данными в формате PCF (Pipe Component File) для трубопроводов.

- **`Source/ProfileImpExp`**  
  Импорт/экспорт профилей (например, продольных профилей трасс).

- **`Source/ProfileView`**, **`Source/ProfileViewCOM`**, **`Source/ProfileViewExtended`**, **`Source/ProfileViewObjects`**  
  Модули работы с продольными профилями: отображение, расширения, COM‑слой и объекты.

- **`Source/CADLibNavisWorkExporter`**  
  Экспорт в Navisworks через CADLib.

---

### 8. Просмотр, визуализация, веб‑сервисы

- **`Source/Visualizer`**, **`Source/VisualizerBridge`**, **`Source/VisualizerUsageEx`**  
  Визуализатор 3D‑модели, мост к нему и примеры использования.

- **`Source/ViewerComponent`**  
  Компоненты для просмотра моделей (отдельный viewer или встраиваемый элемент).

- **`Source/HttpServer`**  
  Встроенный HTTP‑сервер для интеграций, web‑API или удалённого доступа.

- **`Source/WebLibDirectUnmanaged`**, **`Source/WSDirect`**  
  Unmanaged‑доступ к веб‑библиотекам/веб‑сервисам, прямые вызовы web‑API.

- **`Source/RssReader`**  
  Модуль чтения RSS‑лент (новости, уведомления, обновления).

---

### 9. Сетевые сервисы, TDMS, интеграции

- **`Source/NetService`**, **`Source/NetServiceBridge`**, **`Source/NetServiceDatabase`**  
  Сетевой сервис, мост между приложениями и его база данных.

- **`Source/NetConstruction`**, **`Source/NetConstructionObj`**, **`Source/NetConstructionObjCom`**  
  Подсистема “сетевого строительства” (построение/управление сетевыми проектами), объекты и COM‑слой.

- **`Source/URS`**, **`Source/urs4ADT`**, **`Source/urs4Plant3dManaged`**, **`Source/ursXDataAdapter`**  
  Интеграция с URS, AutoCAD ADT, Plant 3D и адаптер для XData.

- **`Source/p4dAcadProxy`**, **`Source/p4darx-2dlayout`**, **`Source/p4dURSLink`**  
  Прокси и связующие модули для внешних приложений/форматов (семейство p4d).

- **`Source/msTDMS`**  
  Интеграция или собственная реализация TDMS (управление технической документацией/данными).

---

### 10. Прочие модули, тесты, утилиты

- **`Source/ATools`**  
  Набор вспомогательных инструментов и утилит (для разработчиков и/или пользователей).

- **`Source/AXOGen`**  
  Генерация аксонометрических схем/чертежей.

- **`Source/build_profile`**  
  Скрипты и проекты, связанные со сборкой/профилированием решения.

- **`Source/CabinetVisualizer`**  
  Визуализатор шкафов/панелей (электрические шкафы, щиты).

- **`Source/CascadeMeshPlugin`**  
  Плагин для работы с каскадными/треугольными сетками (meshes).

- **`Source/DatabaseMaintenanceUnmanaged`**  
  Утилиты по обслуживанию БД в unmanaged‑режиме.

- **`Source/ironApp`**, **`Source/ironObj`**, **`Source/ironObjCom`**, **`Source/IronSample`**  
  Подсистема/пример “iron” (возможно, отдельный продукт или экспериментальный модуль), её объекты и COM‑слой.

- **`Source/LibManager`**  
  Менеджер библиотек (каталоги элементов, шаблоны, сборки).

- **`Source/MLTExport`**, **`Source/MLTool`**  
  Экспорт и инструменты для формата/модуля MLT.

- **`Source/MSLibHost`**  
  Хост для библиотек Model Studio (управление загрузкой/исполнением модулей).

- **`Source/msMPHS`**  
  Специализированный модуль (по названию — гидравлика/теплофизика или расчётная подсистема; детали в коде).

- **`Source/msPDF`**  
  Работа с PDF (печать, экспорт, генерация PDF‑документов).

- **`Source/msTPM`**  
  TPM‑модуль (управление проектами, ресурсами или оборудованием; зависит от конкретной реализации).

- **`Source/projectcs`**  
  Проекты/примеры для работы с модулем проектов (или демонстрационные решения).

- **`Source/Reporter`**, **`Source/ReporterUnmanaged`**  
  Модули отчётов (см. также раздел 7) и их unmanaged‑вариант.

- **`Source/TestApp`**, **`Source/TestUnmanaged`**  
  Приложения для тестирования функциональности (managed и unmanaged).

- **`Source/rvm`**, **`Source/rvmManager`**, **`Source/rvmXchange`**, **`Source/rvmXChangeUI`**  
  Работа с форматом RVM (обычно связан с AVEVA PDMS/E3D): импорт/экспорт, управление, UI.

- **`Source/sccsUtil`**  
  Утилиты, связанные с системами контроля версий/сервисами SCCS.

- **`Source/TowerInterchangeability`**, **`Source/TowerMaster`**  
  Модули, связанные с башнями/мачтами (ЛЭП, связи), взаимозаменяемостью элементов башен.

- **`Source/ActiveDirectoryServices`**  
  Интеграция с Active Directory (пользователи, группы, права).

---

### 11. Конфигурация проектов Visual Studio и бат‑файлы

- **`Source/vs10_ac_*.props`**, **`Source/vs11_*.props`**, **`Source/vs14_*.props`**, **`Source/vs15_*.props`**, **`Source/vs16_*.props`**  
  Общие property‑файлы Visual Studio для разных версий и конфигураций (общие настройки, пути include/lib, макросы).

- **`Source/StartVS16_NCProject.bat`**,  
  **`Source/StartVS16_NCProject23.bat`**, **`Source/StartVS16_NCProject24.bat`**,  
  **`Source/StartVS16_NCProject241.bat`**, **`Source/StartVS16_NCProject25.bat`**  
  Бат‑файлы для запуска типового решения NCProject в разных конфигурациях (NCAD‑версии, отладка/релиз).

- **`Source/VTHEntryAPI`**  
  Точка входа API для подсистемы VTH (специализированный модуль, детали — в исходниках).

---

Этот документ даёт **полную карту верхнеуровневых модулей в `Source`**.  
Если нужно, можно сделать отдельные подробные `.md`‑файлы по конкретным подсистемам (например, `mstPipeCore`, `ViperCS`, `mstProject*`), разобрав их внутренние подпапки и ключевые `.h/.cpp` файлы.


