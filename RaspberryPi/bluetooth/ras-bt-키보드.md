라즈베리 파이에서 블루투스 키보드를 연결하는 방법을 단계별로 설명해드리겠습니다.  

---

### 📌 **1. 블루투스 지원 여부 확인**  
라즈베리 파이 3 이상은 기본적으로 블루투스를 지원합니다.  
만약 라즈베리 파이 2 이하를 사용 중이라면, 별도의 블루투스 동글이 필요합니다.  

### 📌 **2. 블루투스 서비스 활성화**  
터미널을 열고 다음 명령어를 입력하여 블루투스 서비스를 활성화합니다.  
```bash
sudo systemctl enable bluetooth
sudo systemctl start bluetooth
```

블루투스가 정상적으로 실행 중인지 확인하려면:
```bash
systemctl status bluetooth
```
**"active (running)"** 상태인지 확인하세요.

---

### 📌 **3. 블루투스 장치 검색 및 연결**  
1. **블루투스 설정 모드 진입**
   ```bash
   bluetoothctl
   ```
   이 명령어를 실행하면 `bluetoothctl` 콘솔이 열립니다.  
   
2. **블루투스 활성화 및 검색 가능하도록 설정**  
   ```bash
   power on
   agent on
   scan on
   ```
   그러면 주변 블루투스 장치가 검색됩니다.  
   블루투스 키보드가 켜져 있고 페어링 모드인지 확인하세요.

3. **블루투스 장치 목록 확인**  
   ```bash
   devices
   ```
   위 명령어를 실행하면 검색된 블루투스 장치 목록이 표시됩니다.  
   MAC 주소 형식(예: `XX:XX:XX:XX:XX:XX`)으로 키보드가 표시됩니다.

4. **블루투스 키보드 페어링**  
   ```bash
   pair XX:XX:XX:XX:XX:XX
   ```
   입력 후, 키보드에서 화면에 표시된 코드를 입력하고 `Enter` 키를 누르세요.

5. **신뢰할 수 있는 장치로 등록**  
   ```bash
   trust XX:XX:XX:XX:XX:XX
   ```

6. **연결 시도**  
   ```bash
   connect XX:XX:XX:XX:XX:XX
   ```
   정상적으로 연결되었다면 "Connected successfully" 메시지가 표시됩니다.

7. **스캔 중지**  
   ```bash
   scan off
   exit
   ```

---

### 📌 **4. 키보드 자동 연결 설정 (재부팅 후에도 유지)**
```bash
sudo nano /etc/bluetooth/main.conf
```
파일이 열리면 다음 옵션을 찾아 `true`로 변경합니다.
```
AutoEnable=true
```
저장 후 종료(`Ctrl + X → Y → Enter`).

---

### 📌 **5. 연결 확인**
라즈베리 파이를 재부팅한 후, 키보드가 자동으로 연결되는지 확인하세요.  
```bash
sudo reboot
```

만약 자동 연결이 안 된다면 다시 `bluetoothctl`을 실행하여 수동으로 연결해보세요.

---

### ✅ **문제 해결**  
1. **블루투스가 작동하지 않을 때**
   ```bash
   sudo systemctl restart bluetooth
   ```

2. **블루투스 모듈을 다시 불러오기**
   ```bash
   sudo rmmod btusb
   sudo modprobe btusb
   ```

3. **모든 블루투스 설정 초기화**
   ```bash
   sudo bluetoothctl
   remove XX:XX:XX:XX:XX:XX
   ```

4. **블루투스 관련 패키지 업데이트**
   ```bash
   sudo apt update && sudo apt upgrade -y
   ```

---

이제 라즈베리 파이에서 블루투스 키보드를 사용할 수 있습니다! 🚀  
혹시 추가적인 문제가 있다면 말씀해주세요. 😊
