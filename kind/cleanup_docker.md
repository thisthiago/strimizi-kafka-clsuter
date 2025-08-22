# 🐋 Manutenção do Docker Desktop no WSL2

Este guia mostra como liberar espaço em disco usado pelo `docker_data.vhdx`, que é o arquivo de disco virtual do Docker Desktop dentro do WSL2.

---

## 📌 Passo 1 – Encerrar o WSL e o Docker
Antes de otimizar, é importante encerrar todos os processos que usam o WSL e o Docker:

```powershell
# Fecha todas as distribuições WSL em execução
wsl --shutdown

# (Opcional) Feche também o Docker Desktop pelo tray (ícone na barra de tarefas)
````

---

## 📌 Passo 2 – Otimizar o VHDX

Agora, execute o comando para compactar o disco virtual e liberar espaço não utilizado:

```powershell
Optimize-VHD -Path "F:\Docker\DockerDesktopWSL\disk\docker_data.vhdx" -Mode Full
```

👉 Isso **não apaga seus containers, imagens ou volumes**.
Ele apenas reduz o tamanho físico do arquivo `docker_data.vhdx`, removendo blocos livres.

---

## 📌 Passo 3 – Reiniciar o Docker e o WSL

Após a otimização, basta iniciar o Docker Desktop novamente.
Ele automaticamente monta o disco e inicia o WSL.

Ou, se preferir abrir manualmente uma distro WSL:

```powershell
# Inicia a distro padrão do WSL
wsl

# Ou inicia uma distro específica, ex: Ubuntu
wsl -d Ubuntu
```

---

## 🔄 Fluxo resumido

1. `wsl --shutdown`
2. `Optimize-VHD -Path "F:\Docker\DockerDesktopWSL\disk\docker_data.vhdx" -Mode Full`
3. Abrir o **Docker Desktop** ou rodar `wsl` novamente

---
