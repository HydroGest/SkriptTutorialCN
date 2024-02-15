# Skript 入门指北

> 教程作者：*Script Hub* ，译者：*MarkChai* 。

您好，欢迎来到 Skript 的世界！

这是一个通用的"如何 Skript”指南，希望能为您提供配置并开始编写第一个 Skript 脚本所需的一切！本教程包括 *Demon* 最初在原始 [DBO 论坛](https://destiny.bungie.org/forum/) 和 [LimeGlass](https://www.limeglass.com/) 上编写的部分。本教程将假设您熟悉制作 Bukkit 服务器，但不熟悉编程。所以让我们开始吧！

## 什么是 Skript？

> Skript 是 Bukkit/Spigot 的插件，Bukkit/Spigot 是一种流行的 Minecraft 服务器模组，它允许服务器管理员轻松修改 Minecraft 的工作方式，而无需进行任何编程。
>
> *— Peter "Njolbrim" Güttinger*

Skript 由 *Peter Güttinger*（也称为 *Njolbrim* 或 *Njol*）创建，于 2012 年 2 月 16 日首次发布。Skript 的目标是为非程序员提供一种简单的方法来制作自己的微型插件（称为脚本）。Skript 被设计为一种事件驱动的语言。

> 这是通过触发器实现的，其中每个触发器都是条件和效果的集合。每次调用触发器时，都会检查所有条件，如果满足所有条件，则执行效果。
>
> — Peter "Njolbrim" Güttinger

这意味着游戏或服务器中必须发生某些事情才能触发运行你的代码。这些事情被称为**事件**（event）或**触发器**（trigger）。它们可以包括命令、时间流逝或玩家的动作（挖掘方块或跳跃）等内容。在某事发生后，一系列**条件**（condition）和**效果**（effect）就会基于该事件进行实际发生。**条件**是代码向服务器询问的“是”或“否”问题。这可能包括以下内容：玩家是否在线，玩家是否拿着镐。然后发生**效果**，比如给玩家一个物品或移动玩家。这些基本元素与您稍后将学习的其他元素相结合，可以非常快速地为您的服务器生成强大的功能。本教程稍后将深入讨论这些功能。

脚本以以 `.sk` 结尾的文本文件编写。因此，您可以使用任何文本编辑器，例如 VS Code、Sublime Text、NotePad++、Atom 或许多其他编辑器。但是，使用 Microsoft Word 或 Google Drive 将不起作用（强烈不推荐记事本！——译者按）。

还有一个名为 [SkIDE](https://github.com/Scrumplex/SkIDE) 的 Skript IDE，它提供了许多不错的功能，例如自动完成和代码高亮显示。

Skript 的一个非常基本的例子：

```python
# 事件
on join:
    # 效果
    broadcast "欢迎来到 Skript 的世界！"
```

*请注意，#s 用于注释，不会执行任何操作*

每当有人加入服务器时，上面的脚本都会向服务器上的所有在线玩家发送消息“欢迎来到 Skript 的世界！”。您可能会注意到脚本非常容易理解，这是因为 Skript 脚本被设计得特别可读、接近英语且易于理解。

## 配置 Skript

把大象放进冰箱需要几步？

1. 设置基础服务器后，请从以下来源之一下载正确版本的 Skript：

    - **Minecraft 1.9.4 以上**：*bensku* 的分支，2.4x 版本：[https://github.com/SkriptLang/Skript/releases](https://github.com/SkriptLang/Skript/releases)

    - **Minecraft 1.8.x**：

        - *bensku* 的分支（推荐）：[https://github.com/SkriptLang/Skript/releases/tag/dev36](https://github.com/SkriptLang/Skript/releases/tag/dev36")
        
             ⚠ 这个版本适用于 1.9，但也应该适用于 1.8，但是不受支持。

        - *Mirreski* 的分支，修复了 v8b：[https://www.dropbox.com/sh/qubix8i86u216rs/AAATz1mjgYH6ySeUSr0NPYH-a](https://www.dropbox.com/sh/qubix8i86u216rs/AAATz1mjgYH6ySeUSr0NPYH-a)  / [（GitHub仓库）](https://github.com/Mirreski/Skript)

    - **Minecraft 1.7.10 及更早版本**：来自 Njol：[https://dev.bukkit.org/projects/skript/files](https://dev.bukkit.org/projects/skript/files)

    （注：你应该去 [SpigotMC](https://www.spigotmc.org) 下载最新版本，而不是看文档，文档具有时效性。——译者按）

2. 将 `.jar`包 放入服务器的“plugins”目录中。

3. 重新启动服务器一次以生成配置文件和一些示例脚本。

> # 注意
> 
> - *bensku* 的分支不支持 CraftBukkit。它被设计与 Spigot 配合使用，但建议使用 Paper，因为它具有更多功能，并且 Skript 支持其中一些功能，尤其是 timeings v2。
>
> - 所有不是 *Njol* 的 Skript 版本都是非官方的，它们的问题应报告给各自作者的Issue跟踪器。
> 
> - *bensku* 分支的Issue跟踪器：[https://github.com/SkriptLang/Skript/issues](https://github.com/SkriptLang/Skript/issues)
>
> - *Mirreski* 的分叉并不活跃。

## 如何制作脚本？

如前所述，脚本是用以 `.sk` 结尾的文本文件编写的。这些脚本位于 `plugins/Skript/scripts` 文件夹中。您会注意到首次启动 Skript 时生成的几个示例脚本。这些文件的名称中将带有 `-` 前缀，带有此前缀的脚本将被禁用并且不会加载。删除 `-` 前缀将允许加载和运行脚本。

现在让我们制作你的第一个脚本文件！

使用文本编辑器，创建一个名为“hello.sk”的文本文件，并将其保存到 `plugins/Skript/scripts` 文件夹中。请记住，Skript 还会在“scripts”文件夹下的文件夹中加载脚本，例如 `plugins/Skript/scripts/subFolder/test.sk`。现在添加以下文本：

```python
on join:
    broadcast "欢迎来到 Skript 的世界！"
```
并保存文件！

恭喜你刚刚写好了你的第一个脚本！让我们谈谈如何将其加载到服务器上。

## 如何加载脚本？

保存脚本的 sk 文件时不会加载脚本。相反，它们在服务器启动时或使用 `/sk reload` 命令时加载：

```shell
/sk reload hello # 加载名为“hello”的脚本。
 
/sk reload subFolder/hello.sk # 加载名为“hello.sk”且位于“scripts/subFolder/”文件夹下的脚本。

/sk reload subFolder/ # 加载“scripts/subFolder/”文件夹下的所有脚本。

/sk reload scripts # 加载所有脚本。
```

继续尝试吧！现在，当加入您的服务器时，文本“欢迎来到Skript的世界！”将广播给所有的玩家！

脚本的任何错误都将在聊天栏中显示给使用 `reload` 命令的玩家或服务器控制台。与插件不同，使用脚本，您无需重新启动服务器即可添加或更新功能。这一切都可以通过 reload 命令发生。但是，请小心，因为这也可能导致您的服务器出现小小的卡顿，您的玩家在加载大型脚本时可能会遇到这种情况。

现在您可以创建和加载脚本了，让我们进入 Skript 的核心概念！

## Skript 的核心概念

### 事件（Event）

当某事发生时，将调用事件。比如当玩家点击某物受到伤害、死亡时，当生物做某事时，甚至当环境做其他完全独立于实体交互的事情时。这将使您能够在其他事情发生时制造一些事情。例如：、

```python
on explode:
    cancel event
```

注意间距。每当有一个冒号 （`:`） 时，下一行就会再缩进一次。您可以使用制表符或空格作为缩进。缩进的长度无关紧要，但事件必须在每一行上使用相同的缩进。我更喜欢使用 Tab 键，因为我只需要在每次缩进中点击一次。实际代码非常简单。当爆炸发生时，爆炸会被取消。如果您不希望 TNT、苦力怕甚至末影龙破坏您服务器上的东西，这将很有用。请记住，这会取消实际的爆炸事件，这意味着玩家也不会受伤。因此，当爆炸发生时，它会阻止爆炸的发生。您可以轻松地将结果更改为您想要的任何结果。另一个例子可能与杀死服务器上的所有玩家一样戏剧化

### 条件（Condition）

条件是任何脚本的重要组成部分。它们是在执行脚本/触发器（trigger）的其余部分之前检查是否满足条件的代码片段。

条件词的结构如下：

```python
if 条件1:
    # 这段代码将会在条件1成立时运行。
else if 条件2:
    # 这段代码将会在第一个条件不成立且第二个条件成立时运行。
else if 条件3:
    # 这段代码将会在以上两个条件都不成立，且条件3成立时运行。
else:
    # 以上任何条件不成立时运行
 
# Skript还支持内联条件，不支持“else if”和“else”，也不以“if”开头。
# 下面有关于这一点的例子。
```

下面是一个具有权限（permission）的示例：

```python
on right click:
    if player has permission "Skript.boom":
        create explosion with force 3 at targeted block
# 等价于
on right click:
    player has permission "Skript.boom"
    create explosion with force 3 at targeted block
```

这将产生比 TNT 略小的爆炸，但只有在玩家拥有正确的权限时才会这样做。条件也可以用来检查一些事情，比如玩家的库存中是否有物品，或者木牌上的一行说了什么。您甚至可以使用多个条件，以便事件在继续之前必须满足所有条件。

```python
on right click:
    # 条件
    block is a sign
    line 1 of sign is "[商店]"
    player has permission "Skript.shop"
    player has 2 gold nuggets
    # 效果
    remove 2 gold nuggets from player
    give player 1 bread
    message "<light green> 您刚刚买了一个面包。"
```

在这个脚本中，玩家必须右键单击第一行为“[商店]”的木牌、有正确的权限、物品栏里有2个金块。然后效果（effect）就发生了。在这种情况下，玩家将失去 2 个金块并获得一些面包。（尖括号内的内容是颜色控制器——译者按）

### 命令（Command）

在 Skript 中创建命令非常容易。

命令定义的基本模式如下：
```python
command /<命令名称> <参数>:
　　aliases: # 别名
　　executable by: # 执行者
　　usage: # 示例用法
　　description: #  描述
　　permission: # 运行所需的权限
　　permission message: # 权限提示信息
　　cooldown: <时间> # 冷却时间 
　　cooldown message: # 冷却时的提示信息
　　cooldown bypass: # 什么权限可以无视冷却
　　cooldown storage: <变量> # 冷却时间存储在啥变量里
　　trigger: # 触发器
　　　　<要运行的代码>
```
*注意：所有条目都是可选的，包括trigger。*

#### 命令名称 Command Name （必填）

命令名称是命令最基本的基本信息。您可以在命令名称中使用除空格字符以外的任何字符。如果在命令名称中使用空格字符，则空格字符后面的文本将成为参数。 命令名称前的斜杠字符 （`/`） 是可选的（这并不意味着您可以在不带斜杠的情况下执行命令）。

#### 参数 Arguments （可选）

您可以为参数编写任何文本。

您可以通过将参数的某些部分放入 `[方括号]` 中来使它们成为可选参数。

#### 类型参数 Type Arguments

您还可以使用以下模式来限制参数的类型：`<类型 = 默认值>`

例如，您必须输入玩家名称或物品的参数。

- 类型`text/string` 的参数将接受所有内容，`object`类型不能用于参数。
- 类型可以是复数（例如，`number` -> `numbers`，`entity` -> `entities`），以在一个参数中接受多个值。

- `= 默认值`部分是可选的。它使参数成为可选参数，如果执行程序未输入参数，则使用默认值。

- 您还可以使用表达式作为默认值。例如：`<item = %player's tool%>`

示例命令：

```python
command /kill <entity types> [in [the] radius <number = 20>]:
```

这样的话，诸如 `/kill zombies`、`/kill`、`/kill creepers and animals in radius 100` 或 `/kill monsters in the radius 6 in radis 6`的命令都可以调用它。如果未指定，则半径将默认为 20。

#### 别名 Aliases

命令的别名。用逗号分隔。

例：`/alias1`, `alias2`, `/alias3`（斜杠可选）。

#### 可执行者 Executable By

指定可以使用该命令的方式，包括`console`和`players`。

例子：`console`, `players`, `the console and players`。

#### 用法 Usage

如果命令使用不正确，则要发送的消息。比如在您不输入所需的参数，或者当您不使用所需的类型作为类型参数后收到的提示。

你将收到这样的信息：`Correct usage: <the usage message>`

如果未指定此条目，则Usage消息将是用于创建命令的代码。

#### 描述 Description 

命令的说明。其他插件可以获取/显示此内容。

#### 权限 Permission

执行命令所需的权限。如果执行者没有指定的权限，则会发送一条消息。

#### 权限消息 Permission Message

您可以使用此条目编辑默认的无权限消息。

#### 冷却时间 Cooldown

再次使用该命令的冷却时间。示例：
```python
cooldown: 10 seconds
```

请注意，当服务器停止时，命令冷却时间将被重置。若要避免这种情况，请使用 storage 条目。

#### 冷却时间消息 Cooldown Message

顾名思义。

#### 冷却时间旁路 Cooldown Bypass

允许绕过冷却时间的权限。

#### 冷却储存 Cooldown Storage

一个用于存储冷却时间的变量，以便能够使用较长的冷却时间，当服务器停止时不会重置该冷却时间。

#### 触发器 Trigger

如果命令成功执行，则要运行的代码。这必须在`trigger`部分。


#### 如何获取参数？

以下语法用于获取代码中输入的参数：

```bash
[the] last arg[ument][s]
[the] arg[ument][s](-| )%number%
[the] (1st|2nd|3rd|4-90th) arg[ument][s]
[the] arg[ument][s]
[the] %type%( |-)arg[ument][( |-)%number%]
[the] arg[ument]( |-)%type%[( |-)%number%]
```
用法示例
```
the last argument
arg-1
argument 6
13th arguments
the argument
the player argument
arg-item type-3
```

此表达式的返回类型将是参数的类型。所以你可以做到`give arg-1 to player-argument`。

#### 例子

```python
command /give <item> [to] <player=%player%>:
    aliases: /i, /item
    trigger:
        # 我们将第二个参数设置为默认为执行者玩家，
        # 但如果在控制台使用命令，没有玩家，所以第二个参数不会被设置！
        # 不需要检查'执行者是否为控制台'，因为第二个参数将始终尽可能使用执行者玩家，如果没有设置，就表示在控制台使用。
        if arg-2 is not set:
            send "&c请指定一个玩家以给予物品！"
            stop
        # 由于只有一个参数具有“item”类型，我们可以直接使用`item-argument`。
        give item-argument to arg-2
        send "&a已给予玩家&6%arg-2%物品&6%item-argument%&a。"
# 示例：
# /i 64 barriers
# /give dirt Notch
# /give a stone to Notch
```

### 循环（Loop）

循环可用于完成重复性任务，否则这些任务会复杂得多。例如，如果你想看看你附近是否有箱子，你需要检查一定距离内的每个方块，看看它是否是一个箱子。这可以使用循环轻松完成：

```python
command /chest:
    trigger:
        loop blocks in radius 3 around player:
            if loop-block is a chest:
                message "在 %location of loop-block% 处有一个箱子！"
```

百分号表示有一个值将替换该部分的文本。在这种情况下，将显示 x、y 和 z 值，而不是 `%location of loop-block%` 这一串文字（你可以理解为字符串格式控制符——译者按）。`loop-block`是指每次循环时正在检查的方块（这取决于`blocks`，你可以类比为C++里的 `for (auto block: blocks) ` ,Python里的`for block in blocks`。其中`block`就是这里的`loop-block`——译者按）。循环将查看玩家 3 个方块半径内的每个方块，然后运行我们在它下面缩进的代码。而且由于我们使用命令来触发循环，因此我们可以添加参数并允许玩家选择循环的搜索距离。

```python
command /chest <integer=3>:
    trigger:
        loop blocks in radius argument around player:
            if loop-block is a chest:
                message "在 %location of loop-block% 处有一个箱子！"
```
在这里，我们还为命令设置了一个默认值，以防万一玩家没有输入默认值。在循环表达式中，我们看到数字已被替换为“argument”，这意味着您在命令中键入的任何数字都将被放在这里。如果未在此命令中输入数字，则将使用 3，因为它已设置为默认值。如果您想确切地查看半径值有多远，那么您可以使用此脚本从块中制作一个球体，以便您可以明显地看到大小。

```python
command /sphere <integer=3>:
    trigger:
        loop blocks in radius argument around player:
            if loop-block is an air:
                set loop-block to stone
        set {clear location} to location of player
        set {clear radius} to argument
 
command /clear:
    trigger:
        loop blocks in radius {clear radius} around {clear location}:
            if loop-block is stone:
                delete loop-block
            # 删除一个方块意味着将它设置为air（空气）。
```

使用 `/clear` 命令可以轻松删除您创建的球体。另外，因为你将处于球体的中心，所以你需要一种方法将自己传送出去。如果在靠近地面的地方使用，这些命令可能会对您的服务器地图造成少量损坏。请在飞行时使用它们以获得完整的效果。

带有大括号 `{}` 的代码部分称为变量。您将在下一节中了解它们。

## While 循环

While循环是只要指定的条件为真值就运行代码的循环：

```python
while 条件:
    # 代码
```

请注意，当使用while循环时，它们没有延迟，因此比刻（tick）更快，如果在Minecraft中使用方块等东西时没有至少设置一刻延迟，将会导致服务器崩溃：因此请使用`wait a tick`。

用法示例：

```python
# 在文本末尾添加一个点，直到达到10个字符。
on load:
    set {_text} to "文本"
    while length of {_text} is smaller than 10:
        set {_text} to "%{_text}%."
    broadcast {_text} # 文本........
```

### 变量（Variable）

变量用于在名称下存储信息。把它想象成一个带有标签的盒子。当你想得到你放在那个盒子里的信息时，你只需去寻找那个上面有正确标签的信息。Skript 对变量做了同样的事情，变量相当于一个盒子的计算机。您可以像这样保存信息：

```python
set {变量名} to true
```

这样做的原因是为了我们以后可以获得这些信息。因此，也许我们想检查该玩家之前是否执行过命令。我们会这样做：

```python
command /sethome:
    trigger:
        set {home} to location of player
 
command /home:
    trigger:
        teleport player to {home}
```

每次在脚本中使用变量时，都必须将其放在大括号 `{ }` 中，以告诉 Skript 您正在使用变量。上面是一个非常简单的 Home 脚本。我们将玩家的位置存储在一个名为 `{home}` 的变量中：当玩家输入不同的命令（如“`/home`”）时，我们会返回该变量以获取位置，以便我们知道将玩家传送到哪里。这不会清除变量中的值，更像是读取它，然后将其放回原处。在编程时，您始终需要考虑用户/玩家可能做错了什么。例如，玩家以为他们回到了自己的基地，但忘记了设置 Home 。如果他们尝试使用 `/home` 并且没有地方可以传送到哪里会发生什么？这就是要加一行 if 语句的原因。此语句检查某些事件是否正确的运行，如果不是，那么它将执行与脚本其余部分不同的操作。没有默认的错误消息会发送给玩家，因此您需要制作自己的错误消息。

```python
command /sethome:
    trigger:
        set {home} to location of player
 
command /home:
    trigger:
        if {home} is not set:
            message "<red>你还没有设置 Home ！"
            message "<gray>使用 <orange>/sethome <gray> 来设置一个 Home !"
            stop trigger
        teleport player to {home}
```

现在，如果玩家尝试执行 `/home`，他们将收到一条错误消息，然后触发器（trigger）的其余部分将停止。如果你没有添加停止触发器的代码，则 if 语句下未缩进的其余事件将照常继续。此外，如果 if 语句为 false，则不会读取其下缩进的任何代码，并且玩家不会收到错误消息。

我们当前脚本的主要问题是，如果一个人在 `{home}` 变量下设置了他们的 Home 位置，那么任何使用 `/home` 的人都会被传送到该人的 Home，如果有人在另一个玩家之后设置他的 Home ，它将覆盖另一个位置并只保存最新的位置。解决此问题的方法是在变量名称中使用**表达式**。对于命令事件，它是键入命令的人。因此，为了给每个玩家设置不同的 Home，我们实际上可以将玩家的名字放在变量名本身中。

另外，我们应该在这里使用“列表变量（list variables）”。列表变量是一种更简洁的存储值的方式，尤其是某些特定事物（在本例中为玩家）所特有的变量。列表变量可以循环，可以一次性删除，并使变量组织起来。要制作列表变量，我们只需将 `::` 添加到变量名称中： `{home::%player's uuid%}` 这会在 `home` 列表中创建一个变量，使用玩家的 UUID 作为变量名称（index）（你可以理解为字典——译者按） 。

最后，它看起来像这样：

```C++
command /sethome:
    trigger:
        set {home::%player's uuid%} to location of player
 
command /home:
    trigger:
        if {home::%player's uuid%} is not set:
            message "<red>你连 Home 都没设置，传个啥？"
            message "<gray>使用 <orange>/sethome <gray> 来设置一个 Home 。"
            stop # 和 stop trigger 一样。
        teleport player to {home::%player's uuid%}
```

现在，设置其 Home 的玩家姓名也保存在变量名中。例如，当它检查玩家Notch（必须假设该玩家在线）是否设置了home变量时，它将检查` {home::069a79f4-44e9-4726-a5be-fca90e38aaf5}`。有了这个脚本，每个玩家都会有自己独立的 Home 位置。

让我们使用列表变量的一些好处为我们的 Home 脚本制作一些管理命令：

```python
command /resethomes:
    aliases: reset-homes, clearhomes, clear-homes # 别称
    permission: skhomes.admin # 需要的权限
    trigger:
        set {_count} to the size of {home::*}
        clear {home::*}
        send "<light green>成功删除了 <red>%{_count}% <light green>个Home。"
```

`{home::*}`（变量索引带星号）将返回`home`列表中的所有值。我们可以使用 Amount 表达式获取这些变量的数量。

`{_count}`（带有下划线前缀）使变量成为事件的局部变量。无法从其他事件访问局部变量，并将在当前事件结束时删除。

```python
command /listhomes:
    aliases: list-homes, homes
    permission: skhomes.admin
    trigger:
        loop {home::*}:
            # 将UUID转换为具体的玩家并存在{_player}变量中。
            set {_player} to loop-index parsed as an offline player
            send "<orange>%{_player}% 的家： <light blue>%loop-value%"
```

循环列表变量时，`loop-value` 将是当前循环的值而 `loop-index` 将是当前循环变量的索引。在本例中，索引是玩家的 UUID，值是位置。

### 函数（Function）

函数是创建可重用代码部分的有用方法。如果你有一堆经常重复的代码，而不是在很多地方复制和粘贴代码，你可以把它放在一个函数中，然后在需要运行代码时调用该函数。

创建函数时，代码的编写方式与 Skript 中的普通事件类似。

函数的一般格式：
```javascript
function 函数名(参数名: 类型 = 默认值) :: 返回类型:
    # 代码
```

- 函数名称不能包含空格或特殊字符，如 （、`-`、`？`、`.` 或 `/`。但可以包含下划线 （`_`） 和**非英文字母**。

- 可以使用逗号或“and”复制参数。

- 可以使用没有参数的函数。

- `: 类型` 指定要输入的参数的必需类型。

     - 要接受所有类型，可以使用`object`类型。

     - 类型可以是复数（例如，`number` -> `numbers`，`entity` -> `entities`），以在一个参数中接受多个值。

- `= 默认值` 指定如果未输入此参数，将使用的值，因此它使该参数成为可选参数。如果在调用函数时未输入必需的参数，则脚本将在加载时给出错误。

- `:: 返回类型` 如果函数将返回某些内容，则再此设置返回值的类型。确保将 `返回类型` 替换为实际的返回类型（例如 `number`、`text`、`object`、`item`）。

    - 如果将返回列表，则类型可以是复数（例如，`object` -> `objects`、`item` -> `items`）。
    
输入参数在函数代码中作为局部变量。例如，名为 `player` 的参数将为 `{_player}`.

#### 调用函数

调用函数就像使用效果（effect）一样。但如果函数有能力返回某物，也可以像表达式一样使用。

```javascript
函数名(参数)
```

- 可以使用逗号或“and”复制参数

- 若要输入参数的原始列表，它必须位于括号中。否则，它可能会与其他函数参数冲突，因为两者都使用逗号和“and”。如果函数只有一个参数，则不需要这样做。例：`函数名(参数1, (值1, 值2 and 值3), 参数3)`


#### 示例：

```javascript
# 清除聊天
function clearChat(p: player):
    loop 100 times:
        send "" to {_p}

# 用法
command /clearMyChat:
    trigger:
        clearChat(player)

# 发送消息
function sendMessage(players: players, message: text, times: number = 1):
    loop {_times} times:
        send {_message} to {_players::*}

# 用法
sendMessage(player, "message", 10)
sendMessage(all players, "&cmessage")

```

## 附加插件（Addon）

附加插件是由其他开发人员编写的独立插件，用于向 Skript 添加更多功能。插件是 Skript 社区的重要组成部分，您会看到它们无处不在。例如，您可以使用数据库、制作 Discord 机器人、发送网络请求、管理其他插件（如 Citizens 和 WorldGuard）、使用插件产生各种粒子效果等等。要使用插件，您所要做的就是将插件添加到服务器的“plugins”目录中。然后，您可以在重新启动服务器后在脚本中使用它们的语法。

## 在何处查找文档/资源

根据您的 Skript 版本，Njol 的网站或 Bensku 的网站将具有所有最新的原版语法。但是，其他网站（例如 [Skript Hub](https://skripthub.net/)）不仅托管 Skripts 文档，而且将所有附加插件文档都托管在一个地方！这意味着您可以在一个地方搜索每个表达式、条件、效果或事件。两者的链接可以在下面找到：

- 对于原版 Skript：
    - bensku 的 Skript 分支的文档：[https://skriptlang.github.io/Skript/](https://skriptlang.github.io/Skript/)
    - 原始脚本文档：[http://njol.ch/projects/skript/doc](http://njol.ch/projects/skript/doc)
    
- 对于原版 Skript 和附加插件
    - 最新版（推荐）：[https://skripthub.net/docs/](https://skripthub.net/docs/)
    - 旧版：[https://docs.skunity.com/](https://docs.skunity.com/
    )


---

