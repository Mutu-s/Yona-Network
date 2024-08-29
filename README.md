# Yona-Network


1. Gerekli Araçların Kurulumu
Rust ve Solana CLI Kurulumu:

       curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
       sh -c "$(curl -sSfL https://release.solana.com/stable/install)"

       sh -c "$(curl -sSfL https://release.solana.com/v1.10.32/install)"
   
Solana CLI'yi Güncelleyin:

       solana --version
Eğer güncel değilse, yukarıdaki kurulum komutunu yeniden çalıştırın.
![image](https://github.com/user-attachments/assets/b3ad7074-df7a-486b-ba70-2bd39907d474)

2. Proje Oluşturma

       cargo new hello_world --lib
       cd hello_world

Cargo.toml dosyanızı açın ve aşağıdaki bağımlılıkları ekleyin:
      
       nano cargo.toml 

       [package]
       name = "hello_world"
       version = "0.1.0"
       edition = "2021"

       [lib]
       crate-type = ["cdylib"]

       [dependencies]
       solana-program = "1.18.14"



3. Akıllı Sözleşme Kodunu Yazın

        nano src/lib.rs
   
src/lib.rs dosyasına aşağıdaki kodu ekleyin:

       use solana_program::{
       account_info::AccountInfo,
       entrypoint,
       entrypoint::ProgramResult,
       msg,
       pubkey::Pubkey,
       };

       entrypoint!(process_instruction);

       pub fn process_instruction(
       program_id: &Pubkey,
       accounts: &[AccountInfo],
       instruction_data: &[u8],
       ) -> ProgramResult {
       msg!("Hello, world!");
       Ok(())
       }





5. BPF Aracı Kiti ve Çevresel Değişkenler


       wget https://github.com/Snaipe/Criterion/releases/download/v2.3.3/criterion-v2.3.3-linux-x86_64.tar.bz2 -O criterion-v2.3.3-linux-x86_64.tar.bz2
       tar --strip-components 1 -jxf criterion-v2.3.3-linux-x86_64.tar.bz2


Solana toolchain'ını kurun veya mevcut olanı güncelleyin:

      rustup toolchain link solana platform-tools/rust
      
5. Akıllı Sözleşmeyi Derleme
Akıllı sözleşmeyi derleyin:

       cargo build-bpf
Derleme tamamlandığında, ./target/deploy/hello_world.so dosyası oluşturulacaktır.
![image](https://github.com/user-attachments/assets/1f9d95d7-9c9a-4f41-9684-3c407bda4c55)

6. Programı Dağıtma

Yeni bir keypair oluşturmak için:
          
      solana-keygen new --outfile deploy_keypair.json
Parola sorulduğunda boş bırakın (enter'a basın)

Bu pubkey'e bağlı hesaba faucet için Yona Discord'a katılın , #devnet-faucet kanalına gidin ve bu kanala 'faucet' komutunu gönderin
   
7. Yona akıllı sözleşmenizi faucet aldıktan sonra dağıtabilirsiniz
   
       solana program deploy ./target/deploy/hello_world.so -k deploy_keypair.json

![image](https://github.com/user-attachments/assets/8b6c5d48-fbab-4fc0-9512-c2e2187f2a47)

Tebrikler! #
