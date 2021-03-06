# Руководство по стилю проекта <!--- Style Guide -->

*Наиболее разумный подход к Unreal Engine 5*

> **Замечание**: Многие термины будут приведены на английском языке.

> #### "Споры по поводу стиля не имеют смысла. Должно быть руководство по стилю, а вы должны следовать ему."
> [_Rebecca Murphey_](https://rmurphey.com)


## Оглавление: <!--- Table of contents -->


## <a name ="">Основные термины:</a> <!--- Important Terminology -->

#### **Карта / Уровень ( Map / Level )**
Уровень ( Игровая карта ) — отдельная область виртуального мира игры, обычно представляет собой определённую локацию, например, здание или город.

#### **Идентификаторы ( Identifiers )**
Идентификатор — это все, что напоминает или служит «именем». Например, переменная или имя папки, или имя строки таблицы данных и т. д.

#### **Стили**
> #### **camelCase**
>
> "Верблюжий регистр" — по аналогии с горбатым красавцем каждое следующее слово в цепочке начинается с заглавной буквы. Например: `styleGuide`, `eternityProject`.
>
> #### **PascalCase**
>  
> Очень схож с camelCase, но первое слово в строке так же пишется с заглавной буквы. Например: `StyleGuide`, `EternityProject`. 
>
> #### **snake_case**
> 
> «Змеиный регистр» — заменяет пробелы на символ подчеркивания. Например: `style_guide`, `eternity_project`.
>
> #### **SCREAMING_SNAKE_CASE**
> Вариант, в котором все буквы слов пишутся в верхнем регистре. Например: `STYLE_GUIDE`, `ETERNITY_PROJECT`.


## 1 - Соглашение об именовании: <!--- Asset Naming Conventions -->

К соглашению об именовании следует относиться как к закону. Проект, который соответствует соглашению об именовании, может управлять своими ассетами, искать, анализировать и поддерживать их с невероятной легкостью.

### 1.1 - Базовое название - `Prefix_BaseAssetName_Variant_Suffix`: <!--- Base Asset Name -->
Все ассеты должны иметь базовое имя. Оно представляет собой логическую группу связанных ассетов. Любой ассет, являющийся частью логической группы, должен сделовать стандарту `Prefix_BaseAssetName_Variant_Suffix`.

Соблюдение шаблона `Prefix_BaseAssetName_Variant_Suffix` и использование здравого смысла обычно достаточно для создания хорошим имен ассетов. Ниже приведены подробные правила, касающиеся каждого элемента:

* `Prefix` и `Suffix` должны определяться типом ассета, исходя из таблиц Модификаторов имен ассетов.
* `BaseAssetName` должно определяться коротким и легко узнаваемым именем, связанным с контекстом данной группы ассетов. Например, если у вас есть персонаж по имени Илья, то все ассеты Ильи должны содержать `BaseAssetName` == `Ilya`.
* Для уникальных или специфических вариантов ассета используйте `Variant` - это короткое и легко узнаваемое имя, которое представляет логическую группу ассетов, являющихся подмножеством базового имени актива. Например, если у Ильи есть несколько скинов, то эти скины должны по-прежнему использовать `Ilya` в качестве `BaseAssetName`, но включать узнаваемый `Variant`. Скин "Злой" будет называться Ilya_Evil, а скин "Ретро" будет называться Ilya_Retro.
* Для уникальных, но схожих ассетов добавляется нумерующий `Variant` - это двузначное число, начинающееся с `01`. Например, если у Вас есть художник окружения, создающий безымянные камни, они будут называться `Rock_01`, `Rock_02,` `Rock_03` и т. д. За редким исключением, Вам никогда не потребуется трехзначный номер варианта. Если у Вас более 100 ассетов, Вам следует рассмотреть возможность организации их с разными базовыми именами или использованием нескольких вариантов имен.
* В зависимости от того, как создаются варианты ассетов, Вы можете объединять имена вариантов в цепочки. Например, если Вы создаете ассеты напольных покрытий для проекта Motion, Вам следует использовать базовое имя `Flooring` с цепочкой вариантов, таких как `Flooring_Marble_01`, `Flooring_Maple_01`, `Flooring_Tile_Squares_01`.

#### 1.1.1 - Примеры:

#### **1.1.1 E1 - Илья** <!--- Ilya -->
| Тип ассета: ( RU )          | Тип ассета: ( EN )           | Название ассета:                |
| --------------------------- | ---------------------------- | ------------------------------- |
| Скелетный меш               | Skeletal Mesh                | SK_Ilya                         |
| Материал                    | Material                     | M_Ilya                          |
| Текстура ( Diffuse/Albedo ) | Texture ( Diffuse/Albedo )   | T_Ilya_D                        |
| Текстура ( Normal )         | Texture ( Normal )           | T_Ilya_N                        |
| Текстура ( Evil Diffuse )   | Texture ( Evil Diffuse )     | T_Ilya_Evil_D                   |

#### **1.1.1 E2 - Камни** <!--- Rocks -->
| Тип ассета: ( RU )           | Тип ассета: ( EN )         | Название ассета:                |
| ---------------------------- | -------------------------- | ------------------------------- |
| Статичный меш ( 01 )         | Static Mesh ( 01 )         | S_Rock_01                       |
| Статичный меш ( 02 )         | Static Mesh ( 02 )         | S_Rock_02                       |
| Статичный меш ( 03 )         | Static Mesh ( 03 )         | S_Rock_03                       |
| Материал                     | Material                   | M_Rock                          |
| Экземпляр материала ( Снег ) | Material Instance (Snow)   | MI_Rock_Snow                    |

### 1.2 - Модификаторы имён ассетов: <!--- Asset Name Modifiers -->

Используйте эти таблицы наряду с [базовым названием](#base-asset-name), когда именуете ассеты.
Модификаторы имени актива
При присвоении имени активу используйте эти таблицы для определения префикса и суффикса, которые следует использовать в базовом имени актива.

#### 1.2.1 - Часто используемые: <!--- Most Common -->
| Тип ассета: ( RU )      | Тип ассета: ( EN )    | Префикс:      | Суффикс:    | Примечания:                          |
| ----------------------- | --------------------- | ------------- | ----------- | ------------------------------------ |
| Уровень / Карта         | Level / Map           |               |             |                                      |
| Уровень ( Постоянный )  | Level ( Persistent )  |               | _P          |                                      |
| Уровень ( Аудио )       | Level ( Audio )       |               | _Audio      |                                      |
| Уровень ( Освещение )   | Level ( Lighting )    |               | _Lighting   |                                      |
| Уровень ( Геометрия )   | Level ( Geometry )    |               | _Geometry   |                                      |
| Уровень ( Геймплей )    | Level ( Gameplay )    |               | _Gameplay   |                                      |
| Blueprint               | Blueprint             | BP_           |             |                                      |
| Материал                | Material              | M_            |             |                                      |
| Статичный меш           | Static Mesh           | SM_           |             |                                      |
| Скелетный меш           | Skeletal Mesh         | SK_           |             |                                      |
| Текстура                | Texture               | T_            |             |                                      |
| Система частиц          | Particle System       | PS_           |             |                                      |
| Виджет-blueprint        | Widget Blueprint      | WBP_          |             |                                      |

#### 1.2.2 - Анимация: <!--- Animations -->
| Тип ассета: ( RU )             | Тип ассета: ( EN )       | Префикс:    | Суффикс:    | Примечания:               |
| ------------------------------ | ------------------------ | ----------- | ----------- | ------------------------- |
| Сдвиг прицела                  | Aim Offset               | AO_         |             |                           |
| Сдвиг прицела 1D               | Aim Offset 1D            | AO_         |             |                           |
| Blueprint анимации             | Animation Blueprint      | ABP_        |             |                           |
| Композиция анимации            | Animation Composite      | AC_         |             |                           |
| Монтаж анимации                | Animation Montage        | AM_         |             |                           |
| Последовательность анимаций    | Animation Sequence       | AS_         |             |                           |
| Пространство смешивания        | Blend Space              | BS_         |             |                           |
| Пространство смешивания 1D     | Blend Space 1D           | BS_         |             |                           |
| Последовательность уровня      | Level Sequence           | LS_         |             |                           |
| Точка смешивания               | Morph Target             | MT_         |             |                           |
| Paper Flipbook                 | Paper Flipbook           | PFB_        |             |                           |
| Риг                            | Rig                      | RIG_        |             |                           |
| Скелетный меш                  | Skeletal Mesh            | SK_         |             |                           |
| Скелет                         | Skeleton                 | SKEL_       |             |                           |

#### 1.2.3 - Искусственный интеллект: <!--- Artificial Intelligence -->
| Тип ассета: ( RU )         | Тип ассета: ( EN )   | Префикс:      | Суффикс:    | Примечания: |
| -------------------------- | -------------------- | ------------- | ----------- | ----------- |
| ИИ контроллер              | AI Controller        | AIC_          |             |             |
| Дерево поведений           | Behavior Tree        | BT_           |             |             |
| Доска состояний            | Blackboard           | BB_           |             |             |
| Декторатор                 | Decorator            | BTDecorator_  |             |             |
| Сервис                     | Service              | BTService_    |             |             |
| Задание                    | Task                 | BTTask_       |             |             |
| Запрос среды               | Environment Query    | EQS_          |             |             |		
| Контекст запроса среды     | EnvQueryContext      | EQS_          | Context     |             |

#### 1.2.4 - Blueprints:  <!--- Blueprints -->
| Тип ассета: ( RU )             | Тип ассета: ( EN )            | Префикс:       | Суффикс:  | Примечания:                           |
| ------------------------------ | ----------------------------- | -------------- | --------- | ------------------------------------- |
| Blueprint                      | Blueprint                     | BP_            |           |                                       |
| Компонент Blueprint            | Blueprint Component           | BP_            | Component |                                       |
| Библиотека Blueprint-функций   | Blueprint Function Library    | BPFL_          |           |                                       |
| Blueprint-интерфейс            | Blueprint Interface           | BPI_           |           |                                       |
| Библиотека Blueprint-макросов  | Blueprint Macro Library       | BPML_          |           | Рекомендуется не использовать макросы |
| Перечисление                   | Enumeration                   | E              |           | Без нижнего пробела                   |
| Структура                      | Structure                     | F или S        |           | Без нижнего пробела                   |
| Учебный Blueprint              | Tutorial Blueprint            | TBP_           |           |                                       |	
| Blueprint-виджет               | Widget Blueprint              | WBP_           |           |                                       |

#### 1.2.5 - Материалы: <!--- Materials -->
| Тип ассета: ( RU )               | Тип ассета: ( En )               | Префикс:      | Суффикс: | Примечания:                |
| -------------------------------- | -------------------------------- | ------------- | -------- | -------------------------- |
| Материал                         | Material                         | M_            |          |                            |
| Материал пост-обработки          | Material ( Post Process )        | PP_           |          |                            |
| Функция материалов               | Material Function                | MF_           |          |                            |
| Экземпляр материала              | Material Instance                | MI_           |          |                            |
| Материал Parameter Collection    | Material Parameter Collection    | MPC_          |          |                            |
| Профиль подповерхности           | Subsurface Profile               | SP_           |          |                            |
| Физический материал              | Physical Materials               | PM_           |          |                            |
| Декаль                           | Decal                            | M_, MI_       | _Decal   |                            |

#### 1.2.6 - Текстуры <!--- Textures -->
| Тип ассета: ( RU )                  | Тип ассета: ( EN )                    | Префикс:      | Суффикс:    | Примечания:                       |
| ----------------------------------- | ------------------------------------- | ------------- | ----------- | --------------------------------- |
| Текстура                            | Texture                               | T_            |             |                                   |
| Текстура                            | Texture ( Diffuse/Albedo/Base Color ) | T_            | _D          |                                   |
| Текстура ( Нормаль )                | Texture ( Normal )                    | T_            | _N          |                                   |
| Текстура ( Грубость )               | Texture ( Roughness )                 | T_            | _R          |                                   |
| Текстура ( Alpha/Прозрачность )     | Texture ( Alpha/Opacity )             | T_            | _A          |                                   |
| Текстура ( Нейтральный свет )       | Texture ( Ambient Occlusion )         | T_            | _AO         |                                   |
| Текстура ( Неровность )             | Texture ( Bump )                      | T_            | _B          |                                   |
| Текстура ( Излучение )              | Texture ( Emissive )                  | T_            | _E          |                                   |
| Текстура ( Маска )                  | Texture ( Mask )                      | T_            | _M          |                                   |
| Текстура ( Блеск )                  | Texture ( Specular )                  | T_            | _S          |                                   |
| Текстура ( Металлик )               | Texture ( Metallic )                  | T_            | _M          |                                   |
| Текстура ( Упакованная )            | Texture ( Packed )                    | T_            | _*          |                                   |
| Текстура-куб                        | Texture Cube                          | TC_           |             |                                   |
| Текстура-медиа                      | Media Texture                         | MT_           |             |                                   |
| Область прорисовки                  | Render Target                         | RT_           |             |                                   |
| Область прорисовки текстуры-куба    | Cube Render Target                    | RTC_          |             |                                   |
| Профиль освещения                   | Texture Light Profile                 | TLP           |             |                                   |

#### 1.2.6.1 - Упаковка текстур <!--- Texture Packing -->
Обычно принято упаковывать несколько слоев текстурных данных в одну текстуру. Примером этого является упаковка Emissive, Roughness, Ambient Occlusion как красный, зеленый и синий канал одной текстуры. Чтобы определить суффикс, просто сложите вместе заданные буквы суффикса сверху, например `_ERO`.

> Допустимо включать слой Alpha/Opacity в альфа-канал Diffuse/Albedo, и поскольку это обычная практика, то добавление `A` к суффиксу `_D` необязательно.

Упаковывать 4 канала данных в текстуру ( RGBA ) не рекомендуется, за исключением маски Alpha/Opacity в альфа-канале Diffuse/Albedo, т. к. текстура с альфа-каналом несет больше накладных расходов, чем без него.

#### 1.2.7 - Разное: <!--- Miscellaneous -->
| Тип ассета: ( RU )             | Тип ассета: ( EN )         | Префикс:    | Суффикс:    | Примечания:                                                   |
| ------------------------------ | -------------------------- | ----------- | ----------- | ------------------------------------------------------------- |
| Анимированное векторное поле   | Animated Vector Field      | VFA_        |             |                                                               |
| Анимация камеры                | Camera Anim                | CA_         |             |                                                               |
| Цветовая кривая                | Color Curve                | Curve_      | _Color      |                                                               |
| Табличная кривая               | Curve Table                | Curve_      | _Table      |                                                               |
| Набор данных                   | Data Asset                 | *_          |             | Префикс основывается на классе                                |
| Таблица данных                 | Data Table                 | DT_         |             |                                                               |
| Вещественная кривая            | Float Curve                | Curve_      | _Float      |                                                               |
| Тип растительности             | Foliage Type               | FT_         |             |                                                               | 
| Эффект физического отклика     | Force Feedback Effect      | FFE_        |             |                                                               |
| Тип растительности             | Landscape Grass Type       | LG_         |             |                                                               |
| Слой ландшафта                 | Landscape Layer            | LL_         |             |                                                               | 
| Данные Matinee                 | Matinee Data               | Matinee_    |             |                                                               |
| Медиапроигрыватель             | Media Player               | MP_         |             |                                                               |
| Библиотека объектов            | Object Library             | OL_         |             |                                                               |
| Перенаправление                | Redirector                 |             |             | Перенаправление должно быть исправлено при первой возможности |
| Атлас спрайтов                 | Sprite Sheet               | SS_         |             |                                                               |
| Статичное векторное поле       | Static Vector Field        | VF_         |             |                                                               |
| Экземпляр Substance Graph      |Substance Graph Instance    | SGI_        |             |                                                               |
| Фабрика экземпляров субстанции |Substance Instance Factory  |	SIF_        |             |                                                               |
| Настройка тач-интерфейса       | Touch Interface Setup      | TI_         |             |                                                               |
| Векторная кривая               | Vector Curve               | Curve_      | _Vector     |                                                               |

#### 1.2.8 - Paper 2D: <!--- Paper 2D -->
| Тип ассета: ( RU )         | Тип ассета: ( EN )         | Префикс:    | Суффикс:    | Примечания:                        |
| -------------------------- | -------------------------- | ----------- | ----------- | ---------------------------------- |
| Набор кадров               | Paper Flipbook             | PFB_        |             |                                    |
| Спрайт                     | Sprite                     | SPR_        |             |                                    |
| Группа атласов спрайтов    | Sprite Atlas Group         | SPRG_       |             |                                    |
| Карта тайлов               | Tile Map                   | TM_         |             |                                    |
| Тайлсет                    | Tile Set                   | TS_         |             |                                    |

#### 1.2.9 - Физика: <!--- Physics --> 
| Тип ассета: ( RU )         | Тип ассета: ( EN )         | Префикс:    | Суффикс:    | Примечания:                       |
| -------------------------- | -------------------------- | ----------- | ----------- | --------------------------------- |
| Физический материал        | Physical Material          | PM_         |             |                                   |
| Физический ассет           | Physical Asset             | PHYS_       |             |                                   |
| Разрушаемый меш            | Destructible Mesh          | DM_         |             |                                   |

#### 1.2.10 - Звуки: <!--- Sounds -->
| Тип ассета: ( RU )         | Тип ассета: ( EN )         | Префикс:    | Суффикс:    | Примечания:                       |
| -------------------------- | -------------------------- | ----------- | ----------- | --------------------------------- |
| Голос диалога              | Dialogue Voice             | DV_         |             |                                   |
| Запись диалога             | Dialogue Wave              | DW_         |             |                                   |
| Звукозапись медиа          | Media Sound Wave           | MSW_        |             |                                   |
| Эффект ревербации          | Reverb Effect              | Reverb_     |             |                                   |
| Затухание звука            | Sound Attenuation          | ATT_        |             |                                   |
| Класс звука                | Sound Class                |             |             |                                   |
| Очерёдность звуков         | Sound Concurrency          |             | _SC         |                                   |
| Композиция звуков          | Sound Cue                  | A_          | _Cue        |                                   |
| Микс звуков                | Sound Mix                  | Mix_        |             |                                   |
| Звукозапись                | Sound Wave                 | A_          |             |                                   |

#### 1.2.11 Графический интерфейс пользователя <!--- User Interface -->
| Тип ассета: ( RU )         | Тип ассета: ( EN )         | Префикс:      | Суффикс:    | Примечания:                       |
| -------------------------- | -------------------------- | ------------- | ----------- | --------------------------------- |
| Шрифт                      | Font                       | Font_         |             |                                   |
| Кисть Slate                | Slate Brush                | Brush_        |             |                                   |
| Стиль виджета Slate        | Slate Widget Style         | Style_        |             |                                   |
| Виджет-blueprint           | Widget Blueprint           | WBP_          |             |                                   |

#### 1.2.12 Эффекты <!--- Effects -->
| Тип ассета: ( RU )         | Тип ассета: ( EN )         | Префикс:    | Суффикс:    | Примечания:                       |
| -------------------------- | -------------------------- | ----------- | ----------- | --------------------------------- |
| Система частиц             | Particle System            | PS_         |             |                                   |
| Материал постобработки     | Material ( Post Process )  | PP_         |             |                                   |