# til
Today I Learned

## kustomize-config-var
Подстановка переменных кастомайзом в текстовое поле конфигмапа
Нужно явное указание, что Configmap.data можно использовать для подстановки
```
varReference:
  - path: data
    kind: ConfigMap        
```
