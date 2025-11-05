# Guia de Instalação do Armbian em TV Box S905x

O Raspberry Pi/Orange PI é ótimo, mas existem meios com custo inferior disponiveis no mercado.
TV Boxes antigas com processadores ARM — como as baseadas em **Amlogic S905x** ou **Rockchip RK3328** — podem ser transformadas em servidores domésticos, mini-PCs Linux ou ambientes de testes extremamente acessíveis.

MInha TV BOX:
- CPU: Amlogic S905x 
- RAM: 1 GB DDR3  
- Armazenamento via microSD  

---

## 🧰 Materiais Necessários

- **TV Box compatível** (
- **Cartão microSD** de pelo menos **8 GB (classe 10)**    
- **PC ou notebook** para gravação da imagem  

---

## 📦 Downloads Necessários

1. **Imagem Armbian** (disponível neste repositório ou no site oficial)  
   👉 [Download Armbian](https://www.armbian.com/download/)  
2. **Balena Etcher** para gravação no microSD  
   👉 [Baixar Balena Etcher](https://www.balena.io/etcher/)

---

## 🧩 Gravação da Imagem Armbian

1. Abra o **Balena Etcher**.  
2. Selecione a imagem `.img.xz` do Armbian.  
3. Escolha o cartão **microSD**.  
4. Clique em **Flash** e aguarde o término.  
5. Ao finalizar, **remova e insira novamente** o cartão.  
6. **Ignore** qualquer janela do Windows pedindo para formatar.

---

## ⚙️ Configurando o Cartão microSD

## Configurando o Cartão microSD para o Armbian
1. Abra a partição legível do cartão microSD no Explorador de Arquivos.
2. Localize e renomeie o arquivo correspondente ao seu dispositivo para `u-boot.ext` na raiz do cartão microSD:
   - `u-boot-s905` (para dispositivos S905)
   - `u-boot-s905x-s912` (para dispositivos S905X e S912)
   - `u-boot-s905x2-s922` (para dispositivos S905X2 e S922)
3. Edite o arquivo `/extlinux/extlinux.conf` com um editor de texto:
   - Comente as linhas referentes ao `rk-3399` adicionando `#` no início.
   - Descomente as linhas referentes ao `aml s9xx` (FDT e APPEND), removendo o `#`.
   - Atualize a linha `FDT` para apontar ao arquivo `.dtb` compatível com seu dispositivo. Exemplo:
     ```plaintext
     # aml s9xxx
     FDT=/dtb/amlogic/meson-gxl-s905x-p212.dtb
     APPEND=root=LABEL=ROOTFS rootflags=data=writeback rw console=ttyAML0,115200n8 console=tty0 no_console_suspend consoleblank=0 fsck.fix=yes fsck.repair=yes net.ifnames=0

Salve e feche o arquivo.


Remova o cartão microSD com segurança.

Passo 2: Inserir o Cartão microSD

### 3. Inserir o cartão na TV Box
Desligue o aparelho, insira o cartão e ligue.

### 4. Primeiro boot
Aguarde o Armbian iniciar. Usuário padrão: `root`, senha: `1234` SSH.

Notas

Certifique-se de selecionar o arquivo .dtb correto para seu dispositivo para evitar problemas de compatibilidade.
Caso o Armbian não inicialize, verifique as configurações do arquivo extlinux.conf e o nome do arquivo u-boot.ext.

🙏 Agradecimentos
Um agradecimento especial à comunidade de desenvolvedores e colaboradores do Armbian, cujo trabalho possibilita transformar TV Boxes em computadores Linux ficientes.
