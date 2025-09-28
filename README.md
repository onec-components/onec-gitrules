# onec-gitrules

![License](https://img.shields.io/gitlab/license/onec-components/onec-gitrules)
![GitLab Last Commit](https://img.shields.io/gitlab/last-commit/onec-components/onec-gitrules)
[![GitLab Release](https://img.shields.io/gitlab/v/release/onec-components/onec-gitrules)](https://gitlab.com/explore/catalog/onec-components/onec-gitrules)
[![Telegram](https://telegram-badge.vercel.app/api/telegram-badge?channelId=@pravets_IT)](https://t.me/pravets_it)

Компонент Gitlab CI/CD для сборки правил конвертации 1С с помощью утилиты [gitrules](https://github.com/otymko/gitrules). Для сборки используется [Docker-образ gitrules](https://hub.docker.com/r/sleemp/gitrules) из проекта [oscript-images](https://github.com/pravets/oscript-images)

## Пример использования

```yaml
stages:
  - build
  - release

include:
  - component: $CI_SERVER_FQDN/onec-components/onec-gitrules/build-conversion-rules@1.0.2
    inputs:
      input_dir: "src/conv.xml"
  - component: $CI_SERVER_FQDN/onec-components/onec-gitrules/release-conversion-rules@1.0.2
```

### build-conversion-rules

Компонент осуществляет сборку правил конвертации при пуше, запросе на слияние и при назначении тега.

При пуше и запросе на слияние на выходе получаем артефакт с правилами и именем файла `rules-CI_COMMIT_SHORT_SHA.xml`.
При сборке при назначении тега получаем файл `rules-CI_COMMIT_TAG.xml`, который затем передается на стадию публикации релиза.

### release-conversion-rules

Компонент осуществляет публикацю релиза при назначении тега.

происходит запуск `build-conversion-rules` и полученный файл правил публикуется на странице релиза.

## Замечание для self-hosted Gitlab-инстансов

Для использования компонента в вашем инстансе, необходимо клонировать репозиторий в проект на вашем инстансе. Подробнее [в документации](https://docs.gitlab.com/ci/components/#use-a-gitlabcom-component-on-gitlab-self-managed)

Также, предполагается, что для инстанса настроен ssl. И в случае, если используются самоподписанные сертификаты, то потребуется дополнительная настройка раннера, чтобы исключить ошибку проверки самоподписанного сертификата.

Процедура настройки раннеров будет описана в документации позднее.
