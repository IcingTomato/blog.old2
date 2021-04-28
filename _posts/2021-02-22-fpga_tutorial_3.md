---
layout: post
title: "The Tutorial for FPGA Player - Episode 3: Sequential Logic"
description: "写给玩家的FPGA入门指南（3）——时序逻辑"
comments: false
keywords: "FPGA"
---

上期教程中介绍了组合逻辑的使用，而本期教程则要来讲讲时序逻辑。

那么当然，第一个要回答的问题就是，组合逻辑电路和时序逻辑电路有什么区别。如果重新考虑之前做过的电路，不难发现一个特点，这些电路都是给定输入，得到输出。只要输入是一定的，输出也就是一定的。所有影响输出的因素只是输入而已。听起来很自然，没有什么问题对吧？甚至可能还觉得奇怪，如果我给定了输出，但是却不能确定输出，那不是乱套了吗？考虑这么一个需求。还是有一盏灯，有一个按钮，现在需要，按下按键，灯点亮，然后一直保持点亮，再按下按键，灯关闭，并保持关闭。不难看出，单独给定输入状态（按键按下或者没有按下）根本没法知道灯是开着还是关着，也就是输出不单单取决于当前输入，还取决于当前的状态。换句话说，电路有了自己的记忆。而在分析时，除了要考虑当前发生的事情，还需要考虑之前发生过的事情， 多了时间维度。这种电路被称为时序逻辑电路。

# 锁存器与触发器

记忆这事在单片机或者任何软件编程环境里都好说啊，无非是一个变量的事情。但是如果说回到电路角度，应该怎么解决这个问题呢？引入新的逻辑门，比如说 存储门什么的东西？其实完全不用，只要用之前在组合逻辑时用过的那些东西就可以做出能够存储状态的电路哦。原理图如下

![](//panzhifei.fun/img/2021/02/22/3/1551044954929-3-1.png)

看着有些奇怪是不是，这种电路应该怎么分析呢？因为一眼看过去似乎找不到什么输入，只有一个输出Q。不妨考虑下其中任意一条线为高或低，随后计算出来其它所有线的电平，发现没有出现逻辑上的冲突，也就是只要保持通电，这些电平就会一直保持这个状态。但是如果这时，由于外部的信号，改变了其中任意一条线的电平，所有的电平都会变化，并一直保持新的状态。所以呢，这也就是能够存储1个bit的电路了。

不过刚刚其实没有说清楚，什么叫由于外部信号改变了电平啊？怎么改变啊？是的，得有一种可靠的方式来修改状态。而这种方式不是唯一的，一种简单的方法如下：

![](//panzhifei.fun/img/2021/02/22/3/1551044957268-3-2.png)

图中有两条信号线，分别是S和R，表示置位（Set）和复位（Reset），分别可以让这个电路保存的值设置为1或者0。比如可以考虑，当前电路里面保存的数值是0，如果S线为1，就会使对应的NOR门状态发生变化 ，进而使得整个电路保存的数值变为1。当然如果本来就是1，那就什么都不会发生。

不过感觉不太对啊，根据以前使用单片机相关电路的经验，一般都是来一条数据线直接传输数据（高或者低）而不是分成S和R分别传输高或者低。毕竟S的时候不能R，R的时候不能S，弄两条线看起来就有些浪费。要实现直接输入数据而不是R、S，也很简单

![](//panzhifei.fun/img/2021/02/22/3/1551044959296-3-3.png)

现在，如果输入为高，那么S为高，R为低，输出就会被设置成高；如果输入为低，那么S为低，R为高，输出就会被设置为低。听起来很棒是不是？完全不是。输出只会复制输入的情况，结果就是变成了一条存在延迟的导线而已。如果输入“消失”，输出也会随之消失，也就没有什么“记忆”可言了。所以还需要有一条线，用来指示当前的输入是否有效，是否需要存储当前的输入。电路修改成如下： 带有写入使能的记忆电路

现在好了，有了一条使能（Enable）线，用来标记输入是否有效。当Enable为高的时候外部的数据可以进入这个记忆电路；而Enable为低的时候，无论输入信号怎么变，输出信号都不会发生变化， 就像是被锁住了一样，于是这种电路的名字，就叫做锁存器。而这种输入数据的就被称为D锁存器，前面那种输入S和R信号的则被称为SR锁存器。

确实，锁存器听起来像是非常可靠的存储设备，也确实在过去被大量使用，但是现在的数字电路设计中大多已经转向使用触发器来代替锁存器。所以这里我们也就来介绍一下触发器。

首先，锁存器存在一个“缺陷”。Enable为低的时候保存信号电平没有问题，然而Enable为高的时候，就有点意思了。Enable为高的时候，其实也就基本是图？中描述的导线的情况，输出就是对输入的简单复制。不如说，这时整个锁存器是“透明”的，输入信号可以直接穿过锁存器达到输出。而触发器，相比于锁存器，就并不是透明的，因为触发器并不依赖于电平来指示是否要写入，而是依赖于时钟的变化。触发器会在时钟从低到高变化（或者从高到低变化，取决于具体使用的触发器）的瞬间，储存输入的数据，并且在其余时间保持这个数值。这里就简单放一下D触发器的原理图，使用和之前同样的分析方法就可以理解其工作原理。如果不能理解，也没有关系吧，会用就行了。

![](//panzhifei.fun/img/2021/02/22/3/1551044961222-3-4.png)

当然，平时用的时候如果都画全这么一个原理图，一来太累，二来也不清晰，所以锁存器和触发器都可以画成单独的符号，需要的时候使用这个符号即可：

![](//panzhifei.fun/img/2021/02/22/3/1551044962977-3-5.png)

总结一下，这里介绍了两种存储元件，一种叫锁存器，一种叫触发器。对于锁存器来说，重要的是电平状态，高电平存储，低电平保持。而对于触发器来说，重要的是时钟边沿，时钟从低到高的瞬间存储，其它情况保持。注：当然也存在极性相反的原件，如低电平存储高电平保持的锁存器和始终从高到低瞬间存储的触发器。另外“触发器”这一名词曾经可以用来指代各种存储元件，包括现在讨论的锁存器也曾经是触发器的一种。而现在，通常而言触发器特指边沿触发的触发器，电平触发的被称为锁存器。其实锁存器和触发器的类型并不止今天介绍的这几种，但是为了保持简洁，这里只讲和我们的目标——FPGA GameBoy最相关的，其它的就不做介绍了。

# 实例1 灯

其实到这里位置，时序电路需要的新的组件已经介绍完了。确实，所有涉及的只不过是锁存器和触发器而已，而这两者本身也无非只是之前的基础逻辑门的组合罢了。然而，虽然说起来只不过是一些逻辑门的组合罢了，有了这两种元件之后，逻辑电路所能实现的功能瞬间强大了很多，电路的设计和分析难度也随之上升了一个台阶。前面的那个实例，还好说，只涉及一个输入和一个输出，本身比较简单，简单凑一凑设计就出来了。而如果要设计更为复杂的东西，还是束手无策。而我这里能做的，就是提供更多例子，帮助大家理解时序逻辑电路常见的“套路”。而这个实例，也就是开始的，按一下开，再按一下关闭的电灯。

首先，这个电路有一个输出，一个输入，分别是电灯的输出和按键的输入。简单考虑下不难注意到，要求里面提到了保持电灯的状态，那也就是需要一个触发器，用来记忆并保持电灯的状态，而电灯的输出直接接入到触发器的输出上。而每当按键按下的时候，电灯的状态可以发生变化，也就是触发器需要在按键按下的时候存储新的状态，那么按键也就是触发器的时钟信号了。新的状态，按照要求就是一个和当前的状态不同的状态：如果现在开着就关掉，如果现在关着就打开。于是新的状态生成也很简单了，当前状态加一个非门。

![](//panzhifei.fun/img/2021/02/22/3/1551044965199-3-6.png)

另外可以考虑下如果这里直接把触发器换成锁存器会发生什么事情。由于锁存器是透明的，在按下按键的时候，锁存器会不断试图存入输入的值，而不难发现输入的值和当前的输出相关，而透明状态下输出又会因为输入而发生变化……结果就是发生了循环，当前状态会不断在打开和关闭（1和0）之前切换，而电灯则是与之对饮进入高速闪烁状态，而最终的状态，则是放开按键时所处的状态，基本而言就是开和关之间随机一种。可以说整个是一团糟了，没有办法使用。透明带来的问题也就是在使用锁存器进行设计时必须考虑的。我们这里之后的设计，都将全部使用触发器完成，不使用锁存器。

这里顺便附上这个电路的Verilog实现，各位有兴趣的话可以在自己的实验平台上做这个实验。但是，由于按键抖动的原因（各位如果玩过单片机、Arduino一类的，应该已经很明白按键抖动是什么了吧？），可能仍然会导致按键按下状态变化多次。还是再说明一次，这里的Verilog代码仅仅只是用来实验用的，看不懂代码含义也没有关系，可以自己试着摸索摸索，不然的话之后也会有具体的介绍。 以上电路对应的Verilog代码

```verilog
module light(
    input key,
    output reg light);

    always@(posedge key) begin
        light <= ~light;
    end
endmodule
```

# 实例2 计数器

计数器，自然也有多种实现方法，不同的实现方法实现出来的计数器也有不同的特性。比如这里，希望能够实现一个不断自增的计数器，也就是数值不断+1。不知道大家还记不记得上一期出现过的加法器呢？它可以实现二进制数的相加。如果我们修改这个加法器，让它永远执行+1的操作，并且把结果喂给加法器的输入，即可实现自增的功能。不过，直接连接肯定是不行的，输出的同时输入也在发生变化，也就是像之前说的那样出现了循环，最后做出的电路也就没有什么太大的意义。需要做的，也就是用触发器把加法器的输入和输出隔离开来，确保不会立即进入输入。而触发器的时钟信号，也就是让触发器保存当前输入的信号，在这里也就真的成了控制计数器速度的时钟。比如说时钟信号是1Hz，也就是每秒会有1个电平从低到高的变化（上升沿），那么触发器就会更新一次，也就是整个计数器按照1Hz的速度向上计数的效果了。

![](//panzhifei.fun/img/2021/02/22/3/1551044969393-3-8.png)

注意到这里的加法器十分简单，简单到只剩下了两个门。上一期为了实现1位数的加法也永乐两个门把？现在只用了两个门却实现了2位数的加法，怎么做到的呢？原因也很简单，因为这里不需要考虑进位，而且也是固定的+1操作，其实整个电路就可以不用从加法器的角度去考虑，而是直接考虑这是一个输入当前计数值，输出下一个计数值的组合电路，其真值表如下：

![](//panzhifei.fun/img/2021/02/22/3/1551044971307-3-9.png)

按照要求，输出永远是输入+1，而实现这个组合逻辑电路，也就只需要两个门就足够了。按照之前的思路，把组合逻辑部分的输入和输出用触发器隔开，也就实现了需要的效果。

这里同样附上Verilog代码

```verilog
module counter(
    input clk,
    output reg [2:0] count);

    always@(posedge clk) begin
        count <= count + 1;
    end
endmodule
```

# 结语

本期简单向大家介绍了时序电路的概念，介绍了时序电路的基本组成部分：触发器和寄存器，并展示了时序电路一个基本的应用：计数器。这期的内容可能也是和以前一样，并不那么容易理解。一下子没理解没关系，再读一遍。一旦明白了，一切就很简单了。而下一期我们则将要介绍数字电路基础中非常重要的一个部分：状态机。状态机是时序电路设计中非常常用的一个“套路”，提供了一种系统的设计时序逻辑电路的方法，而不是只是像现在一样想办法凑。同时它也是本系列教程中，数字电路部分的最后一个主题。在那之后，就可以开始FPGA相关的内容啦。

也许有观众依然不理解，最终要用的就是FPGA，为什么还要费那么大力气来介绍数字电路呢？毕竟FPGA已经把很多东西都抽象了， 开发时使用的也是编程语言，而不是画逻辑门。确实没错，开发FPGA不需要任何我们现在在画的逻辑门。然而，如果没有现在的这些铺垫，就很难理解FPGA最终编程时究竟是在做什么。如果具象的东西都没理解，势必会给抽象表达的理解带来更大的困难。不过为了避免大家学的东西太多头晕，这里我只介绍了和今后FPGA最直接相关的概念，一些不太那么相关的也就没有介绍。各位如果有兴趣自然可以找更多书来看。但是反过来说，这里所有介绍的，都是重中之重，也请各位希望继续跟着玩的，务必理解这些内容。
