# kubernetes-cheat-sheet

# Nodes

1-) Node'ların listelenmesi

```kubectl get nodes``` ve(ya) ```kubectl get no```

### Not: Diğer örneklerde de göreceğiniz gibi, bazı parametreler varsayılan olarak kısaltmalara sahiptir. İki kullanımın output olarak herhangi bir farkı yoktur.


<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/1.png" width="450">


2-) Node'lar hakkında bilgi alma

```kubectl describe nodes``` ```kubectl describe no```

Herhangi bir node adı belirtilmediğinde mevcut cluster üzerinde çalışan tüm node'lar sırasıyla listelenir. Argüman olarak bir node adı verildiğinde ise o node'a ait detaylı bilgiler görüntülenir.

<img src="https://github.com/DenizParlak/kubernetes-cheat-sheet/blob/master/ss/2.png" width="450">

