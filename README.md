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

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/3.png" width="450">


# Pods

1-) Yeni Pod oluşturma

```kubectl create -f dosya_adı``` ve(ya) ```kubectl apply -f dosya_adı```

### Not: create "Imperative", apply "Declarative" mantığıyla çalışır.

Pod oluşturulurken mevcut YAML dosyası kullanlabileceği gibi "run" ve belirleyici diğer parametreler ile birlikte de aynı işlem gerçekleştirilebilir.

```kubectl run pod_adı --image=redis```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/27.png" width="450">


2-) Pod'ların listelenmesi

```kubectl get pods``` ve(ya) ```kubectl get po```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/5.png" width="450">

"-o wide" kullanımı pod'lar için de geçerlidir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/6.png" width="450">

"--show-labels" kullanımı burada da geçerlidir. Label bilgisine göre "-l" parametresi ile filtreleme yapılabilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/17.png" width="450">


3-) Pod'lar hakkında bilgi alma

```kubectl describe pods``` ve(ya) ```kubectl describe po```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/7.png" width="450">

Pod adı belirtilmediği sürece tüm pod'ların bilgisi listelenir. Özellikle troubleshooting gerektiren durumlarda ilk başvurulan komutlardan birisidir.

4-) Pod'ların silinmesi

```kubectl delete pods``` ve(ya) ```kubectl delete po```

Çoklu silmeler için Pod isimleri aralarında boşluk bırakalarak tanımlanabilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/28.png" width="450">


# Namespaces

1-) Yeni namespace oluşturma

```kubectl create namespace namespace_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/29.png" width="450">

2-) Namespace'lerin listelenmesi

```kubectl get namespaces``` ve(ya) ```kubectl get ns```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/8.png" width="450">

"-o yaml" parametresi namespace'ler için de aktiftir.

3-) Namespace'ler hakkında bilgi alma

```kubectl describe namespaces``` ve(ya) ```kubectl describe ns```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/9.png" width="450">

4-) Namespace'lerin silinmesi

```kubectl delete namespace namespace_adı``` ve(ya) ```kubectl delete ns namespace_adı```


# Deployments

1-) Yeni Deployment oluşturma

```kubectl create deployment deployment_adı --image=imaj_adı```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/30.png" width="450">


2-) Deployment'ların listelenmesi

```kubectl get deployments``` ve(ya) ```kubectl get deploy```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/10.png" width="450">

Kullanılan Docker imajları ve "selector" bilgisi "-o wide" ile görüntülenebilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/11.png" width="450">


"-o yaml" parametresi aynı şekilde Deployment'lar için de kullanılabilir.

3-) Deployment'lar hakkında bilgi alma

```kubectl describe deployments``` ve(ya) ```kubectl describe deploy```

Yine troubleshoot durumlarında kullanılan başlıca komutlardan birisidir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/12.png" width="450">

4-) Deployment'ların silinmesi

```kubectl delete deployments deployment_adı``` ve(ya) ```kubectl delete deploy deployment_adı```


# Services

1-) Yeni Service oluşturma

```kubectl create service loadbalancer mylb --tcp="80:8080"```

Ana şablon "kubectl create service" ile başlar, sonrasında service tipi belirtilmelidir. Bu örnekte "loadbalancer" tipi seçilmiştir. Diğer tipler:

- clusterip
- externalname
- nodeport

Sonrasında service adı ve port tanımlanır.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/31.png" width="450">


1-) Service'lerin listelenmesi

```kubectl get services``` ve(ya) ```kubectl get svc```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/13.png" width="450">

"-o wide" parametresi "selector" bilgisini getirir. "-o yaml" kullanımı servisler için de geçerlidir.

"--show-labels" parametresi ile servise atanan label bilgileri de görüntülenebilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/15.png" width="450">


2-) Service'ler hakkında bilgi alma

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


# ReplicaSets

1-) ReplicaSets listelenmesi

```kubectl get replicasets``` ve(ya) ```kubectl get rs```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/25.png" width="450">

2-) ReplicaSets hakkında bilgi alma

```kubectl describe replicasets``` ve(ya) ```kubectl describe rs```

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/26.png" width="450">


# Events

1-) Event'ların listelenmesi

```kubectl get events``` ve(ya) ```kubectl get ev``` 

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/20.png" width="450">

2-) Event'ların anlık takip edilmesi

```kubectl get events -w``` ve(ya) ```kubectl get ev -w``` 



## İpuçları

Component'ler farklı namespace'ler altında oluşturulmuş olabilir, listelemeler varsayılan olarak "default" namespace'i baz alınarak yapılır. Bu tarz durumlarda "-n" parametresi ile hedef namespace belirtilir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/19.png" width="450">



