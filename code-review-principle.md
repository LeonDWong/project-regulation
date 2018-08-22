# Code Review Principle

### 1、用于review的代码片段，不要透漏其作者，也不要有人去主动认领

因为review的目的不是为了blame，而是针对代码的好坏来进行讨论，透漏代码作者是没有意义的，并且可能在知道代码所有者之后，会影响参会者个人的判断。主持人也要保证代码内不要透漏个人的信息。（会后要不要透漏，可以在讨论）

### 2、一次code review的会议时间不应该超过60分钟

研究表明，需要高度集中力的会议，参与人在60分钟后会开始走神，只是效率下降，故而一次review应该限制在一小时内，高效的进行。

### 3、用来review的代码片段不应超过400行

据统计，200到400行的代码量，对于参会者在一次review中的发现的缺陷密度较高。故而，不应该选择过多的代码，而是注重review代码的质量。

### 4、目标性原则

每次开会前，可以通过eslint等工具来先检测一次代码的defect总数，每行defect数。在开会的最后截断，现场修复代码，以修复70%-90%的代码缺陷为目标。

### 5、有对应的工具来跟踪

进行code review，通过交流改善团队代码规范，并通过相关工具进行记录和校验，目前使用eslint，通过更新.eslintrc文件来更新规则。

### 6、记录checklist

checklist是包含good part，bad part，puzzle part三种的代码风格标准的list。作为一个长期维护的列表，主持人可以根据这个列表，在每次code review，快速定位已经确定的good part，bad part的代码，避免重复的问题的提出。并且每次code review，一旦有更新，都需要在checklist上同步。

## 参考：

[best-practices-for-peer-code-review](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/)