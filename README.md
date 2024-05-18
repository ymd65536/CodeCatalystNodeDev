# Amazon CodeCatalystでNode.jsの環境を構築する

## 構成

- .devcontainer
- .github
- devfile.yaml

## .devcontainerの設定

`devcontainer`の設定ファイルです。

```json
{
	"name": "Ubuntu",
	"image": "mcr.microsoft.com/devcontainers/base:jammy",
	"features": {
		"ghcr.io/cirolosapio/devcontainers-features/alpine-node:0": {}
	}
}
```

## dependabotの設定

```yaml
version: 2
updates:
 - package-ecosystem: "devcontainers"
   directory: "/"
   schedule:
     interval: weekly

```

## 初期のdevfile.yaml

環境構築に使う構成ファイルです。

```yaml
schemaVersion: 2.0.0
metadata:
  name: aws-universal
  version: 1.0.1
  displayName: AWS Universal
  description: Stack with AWS Universal Tooling
  tags: ["aws", "al2"]
  projectType: "aws"
components:
  - name: aws-runtime
    container:
      image: public.ecr.aws/aws-mde/universal-image:latest
      mountSources: true
      volumeMounts:
        - name: docker-store
          path: /var/lib/docker
  - name: docker-store
    volume:
      size: 16Gi
```

## 参考

- [Configuring a devfile for a Dev Environment](https://docs.aws.amazon.com/codecatalyst/latest/userguide/devenvironment-devfile.html)
- [Configuring Codecatalyst Dev Environments](https://repost.aws/articles/ARBTATztMgQOeYyMZ9IAmxDw/configuring-codecatalyst-dev-environments)