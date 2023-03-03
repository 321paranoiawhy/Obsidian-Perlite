
- [Managing Secrets using Configuration File](https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/)
- [Verify the Secret](https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-kubectl/#verify-the-secret)
- [Edit a Secret](https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-kubectl/#edit-secret)

环境变量配置示意:

```yml
- env:
	- name: SECURITY_JWT_SECRET
		valueFrom:
			secretKeyRef:
				name: jwtsecret
				key: secret
```

# `Base64` 编码

```bash
[Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes('1234'))
```

> [!info] '1234' `Bse64` 编码
> MTIzNA==

切至 `config-k8s\k8s\secret` :

> [!note] jwt-secret.yaml
> ```yml
> apiVersion: v1
> kind: Secret
> metadata:
>   name: jwtsecret
> type: Opaque
> data:
>   secret: MTIzNA== # 1234
> ```

```bash
kubectl apply -f jwt-secret.yaml
```

- `data` 字段用于任意数据, 但必须用 `Base64` 编码
- `stringData` 字段数据无需使用 `Base64` 编码
- 如果 `data` 和 `stringData` 同时定义了同一变量, 则 `stringData` 变量值优先级更高 - [Specify both data and stringData](https://kubernetes.io/docs/tasks/configmap-secret/managing-secret-using-config-file/#specify-both-data-and-stringdata)

```yml
data:
  secret: MTIzNA==
```

与

```yml
stringData:
  secret: 1234
```

效果相同。

# 查看已有 `secret`

```bash
kubectl get secrets
```

# 查看 `secret` 详细信息

查看 `test-secret` 详细信息:

```shell
kubectl describe secret test-secret
```