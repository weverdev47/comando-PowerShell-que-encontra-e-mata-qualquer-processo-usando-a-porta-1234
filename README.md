#Comando-PowerShell-que-encontra-e-mata-qualquer-processo-usando-a-porta-1234


Get-Process -Id (Get-NetTCPConnection -LocalPort 1234).OwningProcess | Stop-Process -Force




Como funciona:
1.	Get-NetTCPConnection -LocalPort 1234 → procura qualquer conexão na porta 1234.
2.	.OwningProcess → pega o PID do processo que está usando a porta.
3.	Get-Process -Id ... | Stop-Process -Force → força o encerramento do processo.
Como mudar a porta no LM Studio
1.	Abra o LM Studio (mesmo com erro na porta, você consegue acessar as Configurações/Settings).
2.	Vá em Settings → Server → Port (ou algo parecido, às vezes aparece como Local Server Port).
3.	Mude a porta de 1234 para outra livre, por exemplo:

4321
5678
8765



💡 Dica: Para garantir que a nova porta está livre, você pode checar no PowerShell:

netstat -ano | findstr :4321
•	Se não aparecer nada, a porta está livre.
•	Depois abra o LM Studio, ele deve iniciar sem problemas.

