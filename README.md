Comando PowerShell para encontrar e matar qualquer processo usando a porta 1234 no Windows

Aqui está o **comando PowerShell** para **encontrar e matar qualquer processo usando a porta 1234** no Windows:

### 🔹 Comando direto (recomendado)

Execute o **PowerShell como Administrador**:

```powershell
Get-NetTCPConnection -LocalPort 1234 | ForEach-Object {
    Stop-Process -Id $_.OwningProcess -Force
}
```

### 🔹 Alternativa (mais compatível)

Funciona mesmo em versões antigas do Windows:

```powershell
netstat -ano | findstr :1234
```

Isso vai mostrar algo como:

```
TCP    0.0.0.0:1234    0.0.0.0:0    LISTENING    5678
```

Depois mate o processo pelo **PID**:

```powershell
taskkill /PID 5678 /F
```

### 🔹 Tudo em uma linha (automático)

```powershell
taskkill /F /PID (netstat -ano | findstr :1234 | ForEach-Object { ($_ -split '\s+')[-1] })
```

### ⚠️ Atenção

* Isso **mata qualquer processo** usando a porta 1234
* Use com cuidado se estiver rodando servidores, Docker, Node, Python, etc.

Se quiser, posso adaptar o comando para:

* porta diferente
* mostrar o **nome do processo antes de matar**
* matar só se estiver em **LISTENING**

Só falar 👍
