# onec-gitrules

Компонент Gitlab CI/CD для сборки правил конвертации 1С с помощью gitrules.

## Пример использования

```yaml
stages:
  - build

include:
  - component: $CI_SERVER_FQDN/onec-components/onec-gitrules/build-conversion-rules@1.0.7
    inputs:
      input_dir: "src/conv.xml"
      output_dir: "build/"
```
