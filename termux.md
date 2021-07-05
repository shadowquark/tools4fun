在手机中配置 Termux，而不是单纯使用 WSL/mac/Linux 完成下列操作，主要有几点原因。

1. 对于非专业用户，命令行［CLI］的配置并不友好，使用频率也不会很高。这方面 Termux 只要一行命令就能备份，一行命令就能复原。所以未来我可能会自己制作一个 Termux 镜像，提供我关心的主要功能。但在此之前，我需要总结出哪些功能是实用的。之后，更多人只要解压这个镜像，输入对应命令，就可以直接使用，而不需要复杂的配置过程。暂时我不知道在 WSL/mac/Linux 上如何实现这个效果。尤其随时一个大版本更新，之前安好的东西就坏了。这种『重复配置』的时间成本，应该是很多普通用户无法接受的。
2. 人们用移动设备的时间越来越长，这导致很多实用功能最好能出现在移动设备上，才会变得常用。比如人们可能需要一个随身的多功能科学计算器，最好还能画一些函数图。再有一种可能是人们看到了一个喜欢的视频，想随手下载下来。这些场景，用户往往身边没有电脑，尤其是没有联网的电脑。如果手机能使用 ```youtube-dl``` 和 ```annie``` 一类工具，就可以随手缓存。显然，一个包括矩阵特征值、函数绘图、方程求数值解的 ```jupyter notebook``` 是非常好的科学计算器。我自己在积累这样一个 ```ipython``` 文件，等到我认为它足够实用了，也会放到这个 repo 中。另外，由于 ```WolframEngine``` 目前只有 ```armhf``` 版，没有 ```arm64``` 版，所以无法使用。否则 ```Mathematica``` 是比 ```scipy``` 更好的选择。这样的例子还有很多很多，比如随手用 ```date | md5sum``` 生成密码，然后把密码用 ```GnuPG``` 加密成文件。这样可以自己用本地的 ```master key``` 或 ```private key``` 来管理密码，而不是把所有密码都托付给某个企业的服务器，并心理安慰自己很安全很重视隐私。更多具体的例子会在使用经验分享中逐一介绍。
3. 据我所知，大多数中小学生有个人手机， 但是没有个人电脑。这些工具从小用熟练了，不但具有教育意义，同时会让人在成长过程中看到一个更大、更不一样的世界。我不喜欢用强制手段，把世界改造成我期待的样子。但是很乐于种下使世界有更大概率向我所喜爱的样子去演化的种子。
4. 人们正处于云集算越来越普及的时代，使用更移动的设备、访问更强大的云计算平台，或许是一种技术趋势。显然，Termux 对 ```openSSH``` 的完整支持，超越了其它所有订阅的、付费的、号称自己很强大的 ```SSH``` 客户端。另外，随着折叠屏推向市场，人们也确实开始有更大的屏幕，可以装在口袋中，来完成更复杂的作业，而不是单纯『刷刷刷』。总之，只要 Google 不会发神经在新版 Android 上全面封禁 Termux，其技术特点是面向未来的。
5. 企业对用户的绑架，即企业创造的那种用户无法解脱的对企业的依赖，往往建立在把用户的日常作业转移到『非纯文本』这个手段之上。比如把平平无奇的文档存成 ```doc```，没有专有软件，往往就无法正常显示了。人们在移动端能用到的其它所有针对『纯文本』的软件，可以说加起来都没有 Termux 强大。当一个用户逐渐适应纯文本的时候，适应用 ```git``` 管理纯文本的版本之时，他会自然获得从企业和不得不付费的循环中、解脱出来的自主能力。『纯文本』既是最复杂的，也是最简单的。

下面使用 Termux 的部分，会持续更新。

1. ```Termux-setup-storage``` 可以帮助 Termux 获得整个用户存储的访问权限。参考 [Termux-setup-storage](https://wiki.termux.com/wiki/Termux-setup-storage)。
2. ```vim ~/.termux.termux.properties``` 可以配置 Termux 的外观和行为。比如我配置了一下工具栏 ```extra-keys = [['ESC','TAB','CTRL','ALT','-','LEFT','RIGHT','UP','DOWN']]```。参考 [Terminal Settings](https://wiki.termux.com/wiki/Terminal_Settings)。
3. 用 ```ln -s ~/storage/shared/XXX``` 把手机目录中的 XXX 链接到用户目录，方便快捷访问。最重要的是把 ```/``` 给链接到 ```~```，即 ```ln -s /data/data/com.termux/files/ ~/root```，否则总会显示无法访问 ```cd /```。
4. 使用 ```pkg se``` 搜索，```pkg in``` 安装，```pkg rm``` 卸载，```pkg up``` 更新等等。参考 [Package Management](https://wiki.termux.com/wiki/Package_Management) 获得更多信息。
5. 如前文所述，Termux 最大的优势在于可以方便地备份和恢复。备份只需要
 
  ```
  cd /data/data/com.termux/files
  tar -zcf /sdcard/termux-backup.tar.gz home usr
  ```
  
  恢复只需要
  ```
  termux-setup-storage
  cd /data/data/com.termux/files
  tar -zxf /sdcard/termux-backup.tar.gz --recursive-unlink --preserve-permissions
  ```
  
  就可以实现一次配置，永久使用，随时玩坏了也没负担。参考 [Backing up Termux](https://wiki.termux.com/wiki/Backing_up_Termux)。
6. 
