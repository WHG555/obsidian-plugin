# Obsidian Leaflet

为黑曜石添加可交互的映射功能。医学博士使用[Leaflet.js] (https://leafletjs.com/)

<img src="https://raw.githubusercontent.com/valentine195/obsidian-leaflet-plugin/master/images/7d595a3db9bf0eff9f2a2150819d2bd6956ddcd8.gif">

<img src="https://raw.githubusercontent.com/valentine195/obsidian-leaflet-plugin/master/images/275ff1f560bb6dec0d4fc02b267a7f63860f20c9_2_690x262.jpeg">

概念验证。可能不会像预期的那样工作。目前仅在Windows和Mac上测试。
## 使用插件&示例

地图可以用“传单”代码块创建。例如:

````markdown
```leaflet
id: leaflet-map
image: [[Image.jpg]]
height: 500px
lat: 50
long: 50
height: 500px
minZoom: 1
maxZoom: 10
defaultZoom: 5
unit: meters
scale: 1
marker: default, 39.983334, -82.983330, [[Note]]
darkMode: true
```
````

## 选项

| Option        | Description                                                                          | Default                                    |
| ------------- | ------------------------------------------------------------------------------------ | ------------------------------------------ |
| id            | 唯一标识符(可以是任何东西)。* *必需的。* *                             |                                            |
| image         | 直接URL/文件路径到要用作地图层的图像文件。                 | OpenStreetMap map                          |
| lat           | 渲染时显示的默认纬度。                                     | 50% (image) / 39.983334 (open street map)  |
| long          | 渲染时显示的默认经度。                                       | 50% (image) / -82.983330 (open street map) |
| height        | 地图元素的高度。可以提供像素或窗口高度的百分比. | 500px                                      |
| minZoom       | 地图的最小允许缩放水平。                                        | 1                                          |
| maxZoom       | 地图的最大允许缩放水平。                                         | 10                                         |
| defaultZoom   |地图将加载缩放到这个水平。                                             | 5                                          |
| zoomDelta     | 缩放时，缩放级别将改变此数量。                                | 1                                          |
| unit          | 显示距离的单位                                                        | meters                                     |
| scale         | 用于图像地图距离计算的比例因子。                                    | 1                                          |
| marker        | 在地图上创建不可变的标记                                                |                                            |
| commandMarker | 创建执行命令的不可变标记                                      |                                            |
| markerFile    | 从笔记的正面创建不可变的标记                                 |                                            |
| markerFolder  | 在给定的文件夹中从笔记的_all_中创建不可变的标记                  |                                            |
| markerTag\*   | 使用给定的标记从注释的_all_中创建不可变标记。                |                                            |
| linksTo\*     | 从链接**到**一个音符的音符的_all_创建不可变标记           |                                            |
| linksFrom\*   | 从** from ** a note的_all_中创建不可变标记           |                                            |
| darkMode      | 转化图颜色                                                               | false                                      |
| overlay       | 在地图上添加一个圆形叠加                                                    |                                            |
| overlayTag    |定义要在指定标记注释中搜索的YAML标记                        |                                            |
| overlayColor  | 更改默认覆盖颜色                                                     | blue                                       |
| bounds        |将图像映射边界设置为指定的坐标而不是默认坐标                    |                                            |
| coordinates   | 从笔记中读取位置数据，并使用它作为初始坐标                  |                                            |
| zoomTag       | 从笔记中读取距离缩放数据，并将其作为默认的初始缩放           |                                            |
| geojson       |将GeoJSON文件加载到地图上。                                                       |                                            |
| geojsonColor  |更改GeoJSON特性的默认颜色。                                 | #3388ff                                    |
| gpx           |将GPX文件加载到地图上。                                                           |                                            |
| gpxMarkers    | 设置默认的开始、停止和路标标记                                       |                                            |
| imageOverlay  | 添加一个图像叠加到地图。                                                   |                                            |

> \*: Requires the [DataView plugin](https://github.com/blacksmithgu/obsidian-dataview).

### YAML syntax

从**3.11.0**版本开始，所有参数都可以使用YAML语法定义，而不是使用多个相同的标记。原来的语法仍然可以工作，但是不能将两者合并。

例如:

````
```leaflet
image:
    - [[Image 1]]
    - [[Image 2]]
    - [[Image 3]]
marker:
    - [<type>, <lat>, <long>, <link>]
    - [<type>, <lat>, <long>, <link>]
```
````

#### Marker Tags in YAML

YAML认为' # '符号是一个注释，因此' marktag '参数必须要么用引号括起来(' "#tag" ')，要么定义时不带' # '符号。

另外，' marktag '组的指定方式与之前相同——一个_array_的标签意味着note **必须匹配两个标签**，而_multiple ' marktag '参数将匹配任何标签。请参阅[标记标签](https://github.com/valentine195/obsidian-leaflet-plugin#marker-tags)了解更多信息。
## Map IDs

从**3.0.0**开始，映射id是必需的。如果一个带有旧地图块的注释被打开，插件会警告你这个地图现在需要一个ID。

一旦给了旧映射一个ID，插件将尝试将标记数据与新映射关联起来。

当你更新到3.0.0之后第一次打开插件时，你的标记数据会被备份，以防你需要降级。如果遇到问题，请在Github上创建一个问题。

## 最初的地图视图

### 初始坐标

地图将打开到使用“lat”和“long”定义的纬度和经度。如果没有提供，它将默认为设置中定义的纬度和经度。

或者，可以使用' coordinates '参数定义纬度和经度。坐标可以定义为一个数字数组，也可以定义为具有“location”frontmatter标签的注释的维基链接:

```
coordinates: [36, -89]
coordinates: [[Note with Location Frontmatter]]
```

### 初始缩放级别

地图的初始缩放级别可以使用“defaultZoom”参数设置。这必须是' minZoom '和' maxZoom '参数之间的一个数字-如果在他们之外，它将被设置为最近的参数。

或者，如果定义了“坐标”注释，则可以从该注释的前边读取初始缩放级别为“ ”。

例如，如果一个便条有以下要件:

```
### Note With Frontmatter.md
---
location: [-36, 89]
nearby: 100 mi
---
```

地图是这样定义的:

```leaflet
coordinates: [[Note With Frontmatter]]
zoomTag: nearby
```

然后地图将读取“附近”标签，识别它是“100英里”，并将地图的初始缩放设置为最近的水平，即显示100英里(这取决于“minZoom”，“maxZoom”和“zoomDelta”)。

## 图像映射

### 图像映射URL /文件路径

图像映射可以通过以下三种方式加载:

1. 直接网址(例如:https://i.imgur.com/jH8j3mJ.jpg)
2. Obsidian URL(例如:Obsidian://open?vault=VaultName&file=Path/To/Image.jpg)  
3. 黑曜石图像维基链接(例如，[[image .jpg]])  

### 多映像地图

通过向插件提供多个图像，图像可以在其他图像之上分层:

````markdown
```leaflet
id: Map With Layered Images
image:
    - [[Image1.jpg|Optional Alias]]
    - [[Image2.jpg]]
    - [[Image3.jpg]]
```
````

这将生成一个3层的地图。图1在上面，图2在中间，图3在下面。图像将围绕中心点对齐。  
地图右上角的控制框允许你更改图层。  
标记可以创建和保存在每一层分别从另一个。  
如果给定别名，层控制框将显示给定的名称而不是文件名。  

### 界限

自定义边界可以使用“bounds”参数给图像映射:

````
```leaflet
image: [[Image.jpg]]
bounds:
    - [<top-left-latitude>, <top-left-longitude>]
    - [<bottom-right-latitude>, <bottom-right-longitude>]
```
````

这将导致图像映射的纬度和经度被更新以适应边界。如果提供的边界与图像的宽高比不匹配，这将使图像倾斜地图上定义的任何标记或覆盖将不会更新。

### 图像地图的纬度和经度
因为图像映射没有真正的坐标系统，所以提供的纬度和经度必须以图像左上角**的百分比来给出。  
如果不改变地图的默认缩放级别，这个设置似乎没有任何作用。  

### 单位和规模

如果提供，插件将缩放两个点之间的计算距离' scale '，并显示结果为' xxx单位'。  
在真实的地图上，只有“unit:”是必需的。它将尝试把计量单位从“米”改为“单位”。  

## 标记
可以通过右击将新的标记添加到地图中。  
如果在设置中创建了任何其他标记类型，将出现一个列表供选择。  
一旦创建了标记，就可以将它拖放到不同的位置。    
在地图上创建的标记将被保存到地图实例中。这种方式保存的标记数据将持续存在，只要地图与笔记关联-如果地图块从笔记中删除，或如果所有包含地图块的笔记被删除，与它关联的数据将在7天后删除  

### 标记缩放级别断点
当地图被放大到断点上方或下方时，给定缩放级别断点的标记将从地图上移除。  
这些断点可以在地图上创建的标记的右键菜单中设置，也可以使用源块中创建的标记的参数(更多信息，请参见[在代码块中定义的对象](# Objects - Defined -in-the- Code -block))。  
小心!确保断点在地图的缩放边界内，否则标记可能永远不会显示!  

### 标记的坐标
Alt或Shift-点击一个标记将显示它的坐标。

### 标记链接
记号笔也可以指向笔记;右键单击它，将出现一个弹出窗口。目标可以作为笔记的名称输入。另外，注释中的标头或块可以是标记的目标:
`Note`

`Note#Header1`

如果您有多个同名的音符，您应该指定到该音符的直接路径。否则，地图可能不会打开您期望的那个。  
一旦链接，点击将打开笔记(Ctrl/Cmd-点击在新窗口打开)。  
此外，还可以通过从文件树中拖拽注释并将其放到地图上来创建标记。  
标记链接也可以设置为外部网站。点击标记将打开网站。  
#### Obsidian命令作为链接
还可以通过两种方法之一从命令面板中将标记链接设置为已定义的Obsidian命令。  
命令必须是命令在面板中显示的全名。  

**设置命令的标记链接将在单击标记时执行命令  

> ##### ** 警告* *
>使用命令作为标记目标可能会产生意想不到的后果。
>
>请参考[本期](https://github.com/valentine195/obsidian-leaflet-plugin/issues/38)。

##### 代码块中定义

使用' commandMarker: '而不是' marker: '

##### 在地图上创建
打开“命令标记”开关。
### 批量编辑
从3.9.0版本开始，批量编辑按钮已经添加到映射中。单击此按钮将打开一个模式，允许轻松编辑地图上定义的所有可变标记。

## 覆盖

可以通过Shift-右键，拖动鼠标设置半径，然后再次点击来添加覆盖。点击Escape将取消绘图并删除覆盖。以这种方式添加到地图的覆盖将像标记一样保存到地图实例中，并将在地图重新打开时重新创建。

此外，可以在源块中使用' overlay '参数指定覆盖，如下所示:

`overlay: [<color>, [<lat>, <long>], <radius> <unit?>, <desc>]`

OR

```
overlay:
    - [<color>, [<lat>, <long>], <radius> <unit?>, <desc>]
    - [<color>, [<lat>, <long>], <radius> <unit?>, <desc>]
    ...
```

这将创建一个' ' -覆盖圆，圆心为' ， '，半径' ' in ' '。

> * *请注意* *
> 
>覆盖按指定的顺序绘制。如果较小的覆盖层被较大的覆盖层遮挡，较小的覆盖层将无法交互。

' '可以是任何有效的CSS颜色，包括十六进制，' rgb() '和' hsl() '。

请注意，由于YAML语法，以' # '开头的字符串和以逗号开头的条目必须用引号括起来。

例子:

````
```leaflet
overlay: [blue, [32, -89], 25 mi, 'This is my overlay!']
```
````

````
```leaflet
overlay:
  - ['rgb(255, 255, 0)', [32, -89], 25 km, 'This is also my overlay!']
  - ['#00FF00', [32, -89], 500 ft, 'This is a third overlay!']
```
````

### 编辑叠加

直接绘制在地图上的覆盖可以被编辑。半径和颜色可以改变，或删除覆盖，通过右键单击覆盖。

### 使用Note frontmatter覆盖

与标记类似，覆盖可以从使用' markfile '、' markfolder '和' marktag '参数找到的注释创建。

该插件将扫描笔记的frontmatter，并从frontmatter ' mapoverlay '参数生成一个覆盖，使用与上面相同的语法定义。

### 覆盖标签

覆盖标签参数可以用来自动生成一个覆盖标签在一个笔记的前沿事项。

例子:

````
```leaflet
overlayTag: nearby
```
````

frontmatter注释

```
nearby: 50 km
```

### 叠加颜色

当在地图上绘图或使用叠加标签参数时，叠加颜色标签可用于指定默认的叠加颜色。

## 图像覆盖

可以使用代码块中的' imageOverlay '参数将图像覆盖添加到地图中。

该参数使用以下语法:

````
```leaflet
imageOverlay:
 - [ [[ImageFile|Optional Alias]], [Top Left Coordinates], [Bottom Right Coordinates] ]
 - [ [[ImageFile2|Optional Alias]], [Top Left Coordinates], [Bottom Right Coordinates] ]
 - ...
```
````

这将添加一个位于两个坐标边界之间的图像叠加。如果没有提供坐标边界，覆盖将:

1. 在图像地图上，覆盖整个图像。

2. 在真实地图上，覆盖初始地图视图。

可以使用右上角的图层控制框来切换图像覆盖。类似于带有多个图层的映射，如果提供了可选的别名，图层框将显示别名而不是文件名。


# # GeoJSON

GeoJSON是一种用于描述地理数据结构(如点、线和形状)的格式。有关GeoJSON格式的完整参考信息，请参见[this](https://datatracker.ietf.org/doc/html/rfc7946)。

GeoJSON可以使用以下语法加载到地图中:

````
```leaflet
geojson: [[GeoJSON_File.json]]
```
````

or

````
```leaflet
geojson:
  - [[GeoJSON_File.json]]
  - [[GeoJSON_File_2.json]]
```
````

请注意，GeoJSON是按照提供的顺序绘制的。如果一个小文件与一个大文件重叠，你可能无法与它交互

特别是大的或大量的GeoJSON文件可能会降低初始呈现速度。

### 样式和颜色

GeoJSON特性的默认颜色可以在地图的代码块中使用“geojsonColor”参数定义。此颜色必须是有效的CSS颜色。

此外，映射将尝试读取为GeoJSON特性定义的样式属性以应用样式。样式应该使用[MapBox SimpleStyle规范](https://github.com/mapbox/simplestyle-spec/tree/master/1.1.0)来定义。

### 提示

当鼠标悬停时，地图将尝试读取GeoJSON特性的标题，以显示工具提示。这个标题应该在GeoJSON特性属性的“title”、“description”或“name”字段中定义。

## GPX

GPX，或GPS eXchange，文件可以使用“GPX”参数添加到地图，类似于如何将GeoJSON文件添加到地图。

>想要在黑曜石展示你的Apple Health锻炼?遵循[这些](https://support.apple.com/guide/iphone/share-health-and-fitness-data-iph27f6325b2/ios)步骤，然后将导出的GPX文件添加到您的保险库中，并在地图中使用它们!

````
```leaflet
gpx: [[GPX_File.gpx]]
```
````

or

````
```leaflet
gpx:
  - [[GPX_File.gpx]]
  - [[GPX_File 2.gpx]]
```
````

特别是大的或大量的GPX文件可能会降低呈现速度。

### GPX标记

默认情况下，地图将不会在起点、终点或定义的路径点上显示标记。map可以被告知使用你在设置中定义的标记类型，使用' gpxMarkers '参数:

````
```leaflet
gpx: [[GPX_File.gpx]]
gpxMarkers:
  start: start_marker_type
  end: end_marker_type
  waypoint: waypoint_marker_type
```
````

### GPX样式

目前，GPX只能显示，不能样式化。造型将会在未来更新，包括心跳，速度，海拔等热点。

##代码块中定义的对象

标记和覆盖可以使用以下语法直接在代码块中定义:

| Type    | Syntax                                                                                |
| ------- | ------------------------------------------------------------------------------------- |
| Marker  | `marker: <type*>,<latitude>,<longitude>,<link*>,<description*>,<minZoom*>,<maxZoom*>` |
| Overlay | `overlay: [<color*>, [<latitude, longitude>], <radius*>, <description*>]`             |

可以定义任意数量的对象，但是没有一个对象是可编辑的。_如果需要对这些对象进行更改，则必须编辑代码块。

标记链接可以定义为黑曜石维基链接。

> \*:这些参数是可选的，可以在定义中为空。
>例如，' marker:，25,25…3 '将使用默认的标记类型，纬度和longitude 25，没有链接，没有描述，minZoom 3，没有maxZoom。

**这些将不包括在导出的数据



###标记文件，标记文件夹，标记标记，以及链接中的标记

这些参数允许您直接从指定的注释文件创建标记。

在代码块中可以定义多少个这样的参数是没有限制的;所有找到的文件都将被解析为已定义的标记。

请注意，在我实现某种形式的缓存之前，定义大量的标记文件可能会影响性能

#### 注意Frontmatter

' markfile '， ' markfolder '， ' marktag '， ' linkto '和' linksFrom '参数告诉插件_where寻找notes_。使用笔记frontmatter标签，笔记本身决定了标记是如何创建的。

从笔记中创建的所有标记都将自动将其链接设置为笔记。

| Frontmatter Tag | Use                                                                                             |
| --------------- | ----------------------------------------------------------------------------------------------- |
| location        | 在这个位置创建一个标记。当' coordinates '参数指向此注释时也可使用。 |
| mapmarker       | 将此标记类型用于使用' location '创建的标记。可选的。                       |
| mapzoom         | 从这个笔记创建的标记将其缩放断点设置为' [min, max] '。可选的。      |
| mapmarkers      | 要创建的标记数组。参见下面的语法。                                           |
| mapoverlay      | 要创建的覆盖数组。参见下面的语法。                                            |

#### 的位置

位置标记可以是一组坐标，也可以是一组坐标。每个坐标集将被设置为' mapmarker '类型，任何其他使用位置的标记将使用_first_坐标集。

```
---

location: [25, 25]

# OR

location:
 - [25, 25]
 - [26, 26]
 ...
---
```

##### 地图标记

“mapmarkers”参数可用于定义要在地图上显示的任意数量的标记。这并不需要设置' location '标签。

使用' mapmarkers '定义的标记应该有以下语法:

```
---
mapmarkers:
  - [<type>, [<latitude>, <longitude>], <optional description>, <optional minZoom>, <optional maxZoom>]
  - [<type>, [<latitude>, <longitude>], <optional description>, <optional minZoom>, <optional maxZoom>]
  - ...
---
```

##### 地图覆盖
“mapoverlay”参数可以用来定义任意数量的覆盖来显示在地图上。这并不需要设置' location '标签。

使用' mapoverlay '定义的标记应该有以下语法:

```
---
mapoverlay:
  - [<color>, [<latitude>, <longitude>], <radius> <unit?>, <optional description>]
  - [<color>, [<latitude>, <longitude>], <radius> <unit?>, <optional description>]
  - ...
---
```

如上所示，覆盖的半径应该使用' '(例如' 100英里')来指定。如果没有提供' '，它将默认为' meters '。请参阅[this](src/utils/units.ts)获得支持的单元列表。

#### 标记文件

标记文件可以使用以下语法在代码块中定义:

“markerFile: [[WikiLinkToFile]] ' * *或* *

“markerFile:直接/道路/ /注意'

#### 标记文件夹

标记文件夹可以使用以下语法在代码块中定义:

“markerFolder:直接/道路/ /文件夹”

这将搜索指定文件夹中的所有笔记，甚至子文件夹中的笔记。
#### 标记标签

如果你已经安装了[Dataview plugin](https://github.com/blacksmithgu/obsidian-dataview)，标记也可以使用以下语法从标记创建:

`markerTag: #<tag>, #<tag>, ...`

每个' marktag '参数将返回在该参数中定义了_all_标记的注释。如果你正在查找包含_any_标签的文件，使用单独的' marktag '参数。

如果指定了一个或多个' markerFolder '参数，' markerTag '参数将只在包含tags_的文件夹中查找notes _。

#### 链接

' linkto '和' linksFrom '参数使用DataView的链接索引来查找链接到或来自参数中指定的注释的注释，以构建不可变标记，使用与上面相同的语法。

可以使用YAML数组语法指定多个文件:

```
linksTo: [[File]]
linksFrom:
    - [[File 1]]
    - [[File 2]]
```

#### 例子

```
markerFile: [[MarkerFile]]
```

将

1. 加载MarkerFile。Md记录文件，如果它有正确的frontmatter字段，则为它创建一个标记。
```
markerFile: [[MarkerFile]]
markerFolder: People and Locations
```

将

1. 加载MarkerFile。医学报告
2. 查看人物和地点文件夹以获得更多的注意事项

```
markerTag: #location, #friends
```

将

1. 找到标有“#location”**和“#friends”的所有笔记，并使用他们的frontmatter创建标记

```
markerFolder: People and Locations
markerFolder: Interests/Maps of the World
markerTag: #people, #friends
markerTag: #Paris
```

会搜索笔记吗

1. 文件夹里是人物和地点还是兴趣/世界地图，还有
2. 包含标签#人和#朋友或者标签#巴黎

## 距离

Shift或Alt-点击地图或标记，然后Shift或Alt-再次点击，将显示两点之间的距离。

距离以米为单位显示，除非在地图块中指定了比例因子和/或单位。

地图左下角的控制框显示最后计算的距离。将鼠标悬停在此位置上将显示地图上的距离线，单击它将将地图缩放到这些坐标。

## 黑暗模式

“darkMode”参数将使用CSS反色。这是通过应用a '来完成的。dark mode '的CSS类的贴图贴图层，和以下的CSS:
```css
.leaflet-container .dark-mode {
    filter: brightness(0.6) invert(1) contrast(3) hue-rotate(200deg) saturate(
            0.3
        ) brightness(0.7);
}
```

在自定义代码段中覆盖此CSS将允许自定义黑暗模式外观。关于CSS ' filter '属性的参考，请参阅[本文](https://developer.mozilla.org/en-US/docs/Web/CSS/filter)。

## 设置

### 标记CSV文件

标记数据可以导出到CSV文件。该数据采用以下格式:

| Column 1 | Column 2    | Column 3 | Column 4  | Column 5    | Column 6     | Column 7  |
| -------- | ----------- | -------- | --------- | ----------- | ------------ | --------- |
|地图ID |标记类型|纬度|经度|标记链接|标记层|标记ID |

如果空白，标记类型将默认为“default”。

如果地图只有1层，标记层可以保持空白。

对于新的标记，标记ID可以保留为空。

然后可以重新导入这种格式的标记数据。该功能仍在开发中，可能无法按预期工作。

### 默认标记工具提示行为

设置此值将导致标记工具提示默认为此行为。  
您可以在标记的右键菜单中重写此行为。  

### 默认配置目录

**请备份您的数据。** . Json '文件，然后更改此设置

这个设置将允许你保存数据。将Obsidian . json文件转移到Obsidian配置目录之外的目录。例如，如果您在移动设备和桌面设备上设置了不同的配置目录，那么这将非常有用。数据也将始终保存在默认的Obsidian目录中。

**该插件将保存文件在' <目录>/plugins/obsidian-leaflet-plugin '，就像默认配置

**该目录必须位于您的保险库内

建议者将不会显示隐藏的文件夹;如果你希望插件将数据保存到隐藏文件夹中，你必须手动输入路径。这应该是来自保险库根部的**

### 显示笔记预览

当鼠标悬停链接标记时，使用黑曜石笔记预览。

**请注意，必须启用黑曜石页面预览核心插件才能使用此功能

### 显示覆盖提示

如果禁用，覆盖工具提示默认不会显示。这可以在覆盖上下文菜单中每覆盖一个基础上进行更改。

目前不可能改变这个设置在不可变覆盖。

### 复制坐标按Shift-Click

当Ctrl + Shift-点击地图上的任何位置时，打开此设置将把纬度和经度坐标复制到剪贴板。

### 经度和纬度

如果没有提供，实际地图将打开此默认纬度和经度。

### 默认地图标记

efault标记设置允许您定义一个标记，其他标记可以在其上分层。如果没有添加额外的标记，右键单击地图将放置该标记。
#### 标记图标
[Font Awesome Free](https://fontawesome.com/icons?d=gallery&p=2&s=solid&m=free)图标名称使用。
#### 标记颜色
用于标记颜色的颜色选择器。
#### 图层基础标记
默认情况下，附加标记将在该标记的顶部分层。可以在特定的附加标记上重写此设置。
### 额外的标记
可以添加其他标记类型，可从地图上的上下文菜单中选择。
#### 创建附加标记

添加新的标记将显示一个新窗口，可以在其中添加新的标记参数。

| Parameter    | Description                                                                                          |
| ------------ | ---------------------------------------------------------------------------------------------------- |
| Marker Name  | 当添加标记时显示在上下文菜单中(例如，位置，事件，人物)         |
| Marker Icon  | [Font Awesome Free](https://fontawesome.com/icons?d=gallery&p=2&s=solid&m=free)图标名称使用 |
| Upload Image | 上传自定义图像用于标记图标，而不是使用字体Awesome图标              |
| Layer Icon   | 将这个图标层在基础标记的顶部。如果关闭，将使用图标本身。                   |
| Icon Color   | 覆盖默认图标颜色                                                                 |

如果层图标是打开的，图标可以通过点击和拖动移动到基础图标周围，以自定义图标分层的位置。如果在移动图标时按住Shift，图标将会对齐到中线。

#### 使用图像作为标记图标
当创建一个额外的标记，一个图像可能被上传作为标记图标，而不是选择字体Awesome图标。

点击“上传图片”按钮，选择要使用的图片。插件将加载图像，并将其缩放到“24px x 24px”。用于标记的图像一旦上传，就不能再编辑了。

如果图像已经上传，选择字体Awesome图标将删除图像。

# 版本历史

看到(变更)(https://github.com/valentine195/obsidian-leaflet-plugin/blob/master/CHANGELOG.md)。

# 安装

## 来自黑曜石内部

在Obsidian v0.9.8中，你可以在Obsidian中激活这个插件，方法如下:

-打开设置>第三方插件
-确保安全模式关闭
-单击“浏览社区插件”
-搜索这个插件

——点击安装

-安装完成后，关闭社区插件窗口并激活新安装的插件

## 从GitHub
-从GitHub Repository的Releases部分下载最新版本
-从zip解压插件文件夹到您的保险库的插件文件夹:' <保险库>/.obsidian/plugins/ '

注意:在某些机器上。黑曜石的文件夹可能被隐藏了。在MacOS上，你应该能够按“命令+Shift+点”来显示Finder中的文件夹。

——重载黑曜石

—如果提示安全模式，您可以禁用安全模式并启用插件。

否则转到设置，第三方插件，确保安全模式是关闭和

从那里启用插件。

### 更新

您可以按照相同的步骤来更新插件
# 警告

这个插件没有稳定性的保证，bug可能会删除数据。

请确保您有自动备份。
# TTRPG插件

如果你正在使用Obsidian运行/计划一个TTRPG，你可能会发现我的其他插件有用:

-   [5e Statblocks](https://github.com/valentine195/obsidian-5e-statblocks/) - Create 5e-styled statblocks inside notes
-   [Dice Roller](https://github.com/valentine195/obsidian-dice-roller) - Roll & re-roll dice in notes
-   [Initiative Tracker](https://github.com/valentine195/obsidian-initiative-tracker) - Initiative Tracker view in Obsidian

<a href="https://www.buymeacoffee.com/valentine195"><img src="https://img.buymeacoffee.com/button-api/?text=Buy me a coffee&emoji=☕&slug=valentine195&button_colour=e3e7ef&font_colour=262626&font_family=Inter&outline_colour=262626&coffee_colour=ff0000"></a>
