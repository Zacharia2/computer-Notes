# Dalvik VM虚拟机配置说明

1. heapstartsize——堆初始分配的大小，一个app启动的时候分配的内存大小
2. heapgrowthlimit——分配的一个堆最大的增长值，一个app最多分配的内存大小，超出的话应该会报outofmemory
3. heapsize——整个堆所能达到的最大值，也就是应用程序所能用的内存总和
4. heaptargetutilization——代表堆的利用率，实际使用与最大利用对比
5. heapminfree——堆大小的限制因素，在堆的大小没超过限定值的情况下 最小的空闲值
6. heapmaxfree——和最小相反，堆中最多能空闲的大小
7. lockprof.threshold——调试记录程序内部锁资源争夺的阈值，默认值是500
8. dexopt-flags——程序代码的校验与优化，以下来自百科：
9. dalvik.vm.dexopt-flags： 本参数控制Dalvik虚拟机的程序代码校验和优化。 m为标准选项若m=y则启用不安全代码的校验和托管代码的优化。 兼容性和安全性最高，推荐使用。
   - v为校验选项，可与o并存。 可以是v=a或v=n。若v=a则表示校验所有代码，v=n则关闭代码的校验。
   - o为优化选项，可与v并存。可以是o=v或o=a。 若o=v则表示优化以校验过的代码，o=a则表示优化所有代码。