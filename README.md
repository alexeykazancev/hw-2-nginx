# hw-2-nginx

задание:
    развернуть 4 виртуалки терраформом в яндекс облаке
    1 виртуалка - Nginx - с публичным IP адресом
    2 виртуалки - бэкенд на выбор студента ( любое приложение из гитхаба - uwsgi/unicorn/php-fpm/java) + nginx со статикой
    1 виртуалка с БД на выбор mysql/mongodb/postgres/redis.
    репозиторий в github: README, схема, манифесты терраформ и ансибл
    стенд должен разворачиваться с помощью terraform и ansible
    при отказате (выключение) виртуалки с бекендом система должна продолжать работать

Описание/Пошаговая инструкция выполнения домашнего задания:

В работе должны применяться:

    terraform
    ansible
    nginx;
    uwsgi/unicorn/php-fpm;
    некластеризованная бд mysql/mongodb/postgres/redis.-




если при выполнении команды terraform init возникает ошибка 

Error: Invalid provider registry host
│ 
│ The host "registry.terraform.io" given in provider source address
│ "registry.terraform.io/yandex-cloud/yandex" does not offer a Terraform provider registry

нужно забэкапить файл .terraformrc
затем открыть его и наполнить его следующим содержимым
nano ~/.terraformrc

provider_installation {
  network_mirror {
    url = "https://terraform-mirror.yandexcloud.net/"
    include = ["registry.terraform.io/*/*"]
  }
  direct {
    exclude = ["registry.terraform.io/*/*"]
  }
}

затем повторить инит

при установке mysql.comunity почему-то плагин установился в папку рута, а не пользователя, поэтому долго не выполнялся таск т.к не было модуля, скопировал плагин в пользователся, таск запустился

перераспределить таски и хэндлеры для mysql

при развертывании постгре нужно отдельно вручную задавать пароль на рута

ansible-playbook play_psql.yaml -i hosts_psql --extra-vars "postgres_root_pass=testpas"


DB_HOST