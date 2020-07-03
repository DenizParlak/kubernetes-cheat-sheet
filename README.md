# kubernetes-cheat-sheet

# Nodes

1-) Node'ların listelenmesi

```kubectl get nodes``` ve(ya) ```kubectl get no```

### Not: Diğer örneklerde de göreceğiniz gibi, bazı parametreler varsayılan olarak kısaltmalara sahiptir. İki kullanımın output olarak herhangi bir farkı yoktur.


<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/1.png" width="450">

Aynı komut "-o wide" parametresiyle birlikte kullanıldığında Internal-External IP, işletim sistemi, çekirdek versiyonu ve Docker Runtime bilgileri de gösterilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/3.png" width="450">

"--show-labels" parametresi ile label bilgileri görüntülenebilir. Bu parametreden aldığınız sonucu "--selector" parametresi ile birlikte kullanarak "label" bazlı listeleme yapabilirsiniz.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/16.png" width="450">

Listeme işlemlerinde JSON bazlı filtrelemeler de yapılabilmektedir. Örneğin sadece Internal IP bilgilerini getirmek için:

```kubectl get nodes -o jsonpath='{.items[*].status.addresses[?(@.type=="InternalIP")].address}'```

komutu kullanılır.



2-) Node'lar hakkında bilgi alma

```kubectl describe nodes``` ve(ya) ```kubectl describe no```

Herhangi bir node adı belirtilmediğinde mevcut cluster üzerinde çalışan tüm node'lar sırasıyla listelenir. Argüman olarak bir node adı verildiğinde ise o node'a ait detaylı bilgiler görüntülenir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/2.png" width="450">


Bir node hakkında çok daha ayrıntılı bilgi alabilmek için "get" ile birlikte "-o yaml" parametresi de kullanılabilir. Bu şekilde bilgiler JSON formatında aktarılır.

```kubectl get no -o yaml```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/4.png" width="450">


# Pods

1-) Pod'ların listelenmesi

```kubectl get pods``` ve(ya) ```kubectl get po```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/5.png" width="450">

"-o wide" kullanımı pod'lar için de geçerlidir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/6.png" width="450">

"--show-labels" kullanımı burada da geçerlidir. Label bilgisine göre "-l" parametresi ile filtreleme yapılabilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/17.png" width="450">


2-) Pod'lar hakkında bilgi alma

```kubectl describe pods``` ve(ya) ```kubectl describe po```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/7.png" width="450">

Pod adı belirtilmediği sürece tüm pod'ların bilgisi listelenir. Özellikle troubleshooting gerektiren durumlarda ilk başvurulan komutlardan birisidir.


# Namespaces

1-) Namespace'lerin listelenmesi

```kubectl get namespaces``` ve(ya) ```kubectl get ns```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/8.png" width="450">


"-o yaml" parametresi namespace'ler için de aktiftir.

2-) Namespace'ler hakkında bilgi alma

```kubectl describe namespaces``` ve(ya) ```kubectl describe ns```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/9.png" width="450">

# Deployments

1-) Deployment'ların listelenmesi

```kubectl get deployments``` ve(ya) ```kubectl get deploy```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/10.png" width="450">

Kullanılan Docker imajları ve "selector" bilgisi "-o wide" ile görüntülenebilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/11.png" width="450">


"-o yaml" parametresi aynı şekilde Deployment'lar için de kullanılabilir.

2-) Deployment'lar hakkında bilgi alma

```kubectl describe deployments``` ve(ya) ```kubectl describe deploy```

Yine troubleshoot durumlarında kullanılan başlıca komutlardan birisidir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/12.png" width="450">


# Services

1-) Servislerin listelenmesi

```kubectl get services``` ve(ya) ```kubectl get svc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/13.png" width="450">

"-o wide" parametresi "selector" bilgisini getirir. "-o yaml" kullanımı servisler için de geçerlidir.

"--show-labels" parametresi ile servise atanan label bilgileri de görüntülenebilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/15.png" width="450">


2-) Servisler hakkında bilgi alma

```kubectl describe services``` ve(ya) ```kubectl describe svc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/14.png" width="450">


# DaemonSet

1-) DaemonSet'lerin listelenmesi

```kubectl get daemonset``` ve(ya) ```kubectl get ds```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/18.png" width="450">


2-) DaemonSet hakkında bilgi alma

```kubectl describe daemonset``` ve(ya) ```kubectl describe ds```


# PersistentVolume

1-) PersistentVolume'ların listelenmesi

```kubectl get persistentvolume``` ve(ya) ```kubectl get pv```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/21.png" width="450">

2-) PersistentVolume hakkında bilgi alma

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/22.png" width="450">

# PersistentVolumeClaim

1-) PersistentVolumeClaim'ların listelenmesi

```kubectl get persistentvolumeclaim``` ve(ya) ```kubectl get pvc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/23.png" width="450">

2-) PersistentVolumeClaim'ler hakkında bilgi alma

```kubectl describe persistentvolumeclaim``` ve(ya) ```kubectl describe pvc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/24.png" width="450">



# Events

1-) Event'ların listelenmesi

```kubectl get events``` ve(ya) ```kubectl get ev``` 

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/20.png" width="450">

2-) Event'ların anlık takip edilmesi

```kubectl get events -w``` ve(ya) ```kubectl get ev -w``` 



## İpuçları

Component'ler farklı namespace'ler altında oluşturulmuş olabilir, listelemeler varsayılan olarak "default" namespace'i baz alınarak yapılır. Bu tarz durumlarda "-n" parametresi ile hedef namespace belirtilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/19.png" width="450">



