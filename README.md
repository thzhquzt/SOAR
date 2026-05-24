# SOAR
# 🛡️ Hệ thống SOC/SOAR: Chuỗi Tấn Công Thực Chiến & Phản Ứng Tự Động

## 📖 Tổng quan dự án
Dự án giả lập toàn diện một cuộc tấn công mạng từ khâu xâm nhập (Initial Access), leo thang đặc quyền (Privilege Escalation), khai thác sâu (Post-Exploitation), cho đến khâu điều tra, xử lý sự cố (Incident Response) bằng Wazuh SIEM và tự động hóa quy trình phân tích mối đe dọa qua SOAR (Shuffle).

* **Hồ sơ kỹ thuật chi tiết (Step-by-step cấu hình):** Vui lòng xem file `SOC_SOAR.pdf` trong thư mục `docs/`.

---

## 🚀 Nội dung thực hiện theo các giai đoạn

<details>
<summary><b>🛠️ GIAI ĐOẠN 1: DỰNG LAB & NGHIỆM THU ĐƯỜNG ỐNG GIÁM SÁT</b></summary>
<br>

Xây dựng môi trường mạng Lab khép kín, cấu hình các Custom Rules trên Wazuh và tích hợp các Node chức năng trên Shuffle để đồng bộ dữ liệu về TheHive.

1. **Sơ đồ mạng tổng thể:**
   ![Network Topology](images/1_build_lab/01_network_topology.png)
2. **Kích hoạt trạng thái Wazuh Agent thành công:**
   ![Wazuh Agent Active](images/1_build_lab/02_wazuh_agent_active.png)
3. **Cấu hình Custom Rules trên Wazuh Manager:**
   ![Wazuh Custom Rule](images/1_build_lab/03_wazuh_custom_rule.png)
4. **Cảnh báo (Alert) kích nổ ban đầu trên Wazuh Dashboard:**
   ![Wazuh Initial Alert](images/1_build_lab/04_wazuh_initial_alert.png)
5. **Sơ đồ hoàn chỉnh các Node cấu hình trên Shuffle:**
   ![Shuffle Workflow Complete](images/1_build_lab/05_shuffle_workflow_complete.png)
6. **Nghịêm thu đường ống Pipeline (Ghép Alert Wazuh & TheHive):**
   ![Pipeline Validation](images/1_build_lab/06_pipeline_validation_merged.png)

</details>

---

<details>
<summary><b>🎣 GIAI ĐOẠN 2: TẤN CÔNG XÂM NHẬP & LEO THANG ĐẶC QUYỀN (UAC BYPASS)</b></summary>
<br>

Giả lập chiến dịch Phishing bằng WinRAR SFX ngụy trang file CV. Đóng vai Attacker sử dụng Sliver C2 để thiết lập Session và bypass UAC chiếm quyền Administrator.

1. **Giao diện hòm thư nạn nhân nhận Mail Phishing CV độc hại:**
   ![Phishing Email CV](images/2_attack_escalate/07_phishing_email_cv.png)
2. **File mã độc chứa mồi nhử Double Extension nằm trong máy nạn nhân:**
   ![Malware File On Victim](images/2_attack_escalate/08_malware_on_victim.png)
3. **Sliver C2 trên máy Kali nhận Session điều khiển ngược thành công:**
   ![Sliver Session Established](images/2_attack_escalate/09_sliver_session_established.png)
4. **Thực thi kỹ thuật Leo thang đặc quyền qua `fodhelper.exe`:**
   ![UAC Bypass Fodhelper](images/2_attack_escalate/10_uac_bypass_fodhelper.png)
5. **Kiểm tra quyền tối cao của tài khoản độc hại `backupadmin` vừa tạo:**
   ![Check BackupAdmin Privilege](images/2_attack_escalate/11_check_backupadmin_privilege.png)
6. **Bảng Cảnh báo chuỗi Leo thang đặc quyền (Ghép Alert Wazuh & TheHive):**
   ![Escalation Alert](images/2_attack_escalate/12_escalation_alert_merged.png)

</details>

---

<details>
<summary><b>📦 GIAI ĐOẠN 3: KHAI THÁC SÂU & TUỒN DỮ LIỆU NHẠY CẢM (DATA EXFILTRATION)</b></summary>
<br>

Hacker tiến hành lục lọi hệ thống, trích xuất dữ liệu từ các ứng dụng ghi chú, cơ sở dữ liệu KeePass và thiết lập cơ chế duy trì truy cập (Persistence).

1. **Phát hiện vị trí lưu file nhạy cảm `plum.sqlite` (Sticky Notes):**
   ![Find Plum SQLite](images/3_deep_exploit/13_find_plum_sqlite.png)
2. **Sử dụng SQLite3 bóc tách thông tin ghi chú quan trọng từ file cấu hình:**
   ![Extract Notes Data](images/3_deep_exploit/14_sqlite3_extract_notes.png)
3. **Thực hiện tuồn file cơ sở dữ liệu mật khẩu `.kdbx` về máy Kali:**
   ![KDBX Data Exfiltration](images/3_deep_exploit/15_kdbx_data_exfiltration.png)
4. **Mở KeePass đọc toàn bộ thông tin tài khoản nhạy cảm của hệ thống:**
   ![KeePass Credential Access](images/3_deep_exploit/16_keepass_credential_access.png)
5. **Gõ lệnh Registry thiết lập Backdoor duy trì truy cập ngầm:**
   ![Persistence Backdoor Setup](images/3_deep_exploit/17_persistence_backdoor_setup.png)
6. **Bảng Cảnh báo chuỗi hành vi Khai thác sâu (Ghép Alert Wazuh & TheHive):**
   ![Deep Exploit Alert](images/3_deep_exploit/18_deep_exploit_alert_merged.png)

</details>

---

<details>
<summary><b>🚨 GIAI ĐOẠN 4: ỨNG PHÓ KHẨN CẤP SOC & MỞ RỘNG TỰ ĐỘNG HÓA SOAR</b></summary>
<br>

Trọng tâm phòng tuyến Blue Team: Điều tra hiện trường, thực hiện Eradication (Làm sạch), cấu hình Active Response chặn IP tự động và thiết kế các luồng SOAR nâng cao.

1. **Bảng tổng hợp hành động ứng phó (Cô lập mạng, Đóng băng user, Diệt tiến trình độc):**
   ![Incident Containment Action](images/4_response_expansion/19_incident_response_containment_merged.png)
2. **Bằng chứng điều tra Alert trên TheHive (Bắt quả tang Bypass UAC và User quyetnt):**
   ![Investigation UAC Bypass](images/4_response_expansion/20_investigation_uac_bypass.png)
3. **Nghiệm thu kết quả khắc phục (Tước quyền thực thi, Xóa user backdoor, Xóa ổ bệnh CV):**
   ![Remediation Response Cleanup](images/4_response_expansion/21_remediation_uac_response_merged.png)
4. **Quét X-Ray kiểm tra Dịch vụ (Services) ẩn nấp ngầm:**
   ![X-Ray Service Scan](images/4_response_expansion/22_xray_service_scan.png)
5. **Nghiệm thu rà quét Backdoor rớt lại (Ghép thư mục Startup ẩn và kết nối mạng ra ngoài):**
   ![Backdoor Diagnostic Scan](images/4_response_expansion/23_startup_and_network_backdoor_scan_merged.png)
6. **Rà quét kiểm tra an toàn các khóa Registry và Schedule Tasks:**
   ![Registry ScheduleTask Scan](images/4_response_expansion/24_registry_scheduletask_scan.png)
7. **Bổ sung Code cấu hình tự động block mạng 10 phút vào file `ossec.conf`:**
   ![Wazuh Active Response Config](images/4_response_expansion/25_wazuh_active_response_config.png)
8. **Wazuh phát hiện hệ thống dính lỗ hổng bảo mật nghiêm trọng CVE-2026:**
   ![Wazuh CVE Detection](images/4_response_expansion/26_wazuh_cve_detection.png)
9. **Sơ đồ luồng SOAR thiết kế riêng cho việc phân loại và xử lý lỗ hổng CVE thông minh:**
   ![Shuffle CVE Management Workflow](images/4_response_expansion/27_shuffle_cve_management_workflow.png)
10. **Bản mở rộng luồng SOAR tự động phân tích mã độc (Workflow Extension - Tích hợp API VirusTotal & Any.Run):**
    ![Shuffle Workflow Extension](images/4_response_expansion/28_shuffle_workflow_extension.png)

</details>

---
