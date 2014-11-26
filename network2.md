在上一篇文章中，我们了解了几个网络组件，如openvswitch/network namespace/Linux bridges/veth pairs。这篇文章中，我们将用3个简单的网络场景，展示这些基本网络组件如何以工作从而实现openstack的SDN方案。在这些网络场景中，我们会了解整个网络配置和他们如何一起运行。网络场景如下：
1. 创建网络——我们创建网络时，发生了什么。如何创建多个隔离的网络。
2. 创建虚拟机——一旦我们有了网络，我们可以创建虚拟机并将其接入网络
3. 虚拟机的DHCP请求——opensack可以自动为虚拟机配置IP。通过openstack neutron控制的DHCP服务完成。我们来了解这个服务如何运行，DHCP请求和回应是什么样子的？

这篇文章中，我们会展示网络连接的原理，我们会了解网络包如何从A到B。我们先了解已经完成的网络配置是什么样子的？然后我们讨论这些网络配置是如何以及何时创建的？我个人认为，通过例子和具体实践看到真实的网络接口如何工作以及如何将他们连接起来是非常有价值的。然后，一切真相大白，我们知道网络连接如何工作，在后边的文章中，我将进一步解释neutron如何配置这些组件，从而提供这样的网络连接能力。

We are going to get pretty technical shortly and I recommend trying these examples on your own deployment or using the Oracle OpenStack Tech Preview. Understanding these three use cases thoroughly and how to look at them will be very helpful when trying to debug a deployment in case something does not work.