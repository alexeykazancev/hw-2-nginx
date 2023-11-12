# hw-2-nginx


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