# Hướng dẫn chi tiết thi Certified Kubernetes Administrator (CKA) – cập nhật tháng 6/2026

**Đối tượng sử dụng:** Học viên chuẩn bị thi CKA, đội vận hành Cloud/Kubernetes.  
**Thời điểm cập nhật:** 31/05/2026, dùng cho batch học/thi trong tháng 6/2026.  
**Nguồn ưu tiên:** CNCF, The Linux Foundation, Linux Foundation Training & Certification Docs.

> Note: CKA là chứng chỉ có thông tin thay đổi theo thời gian, đặc biệt là version Kubernetes, chính sách exam simulator, phí thi và quy định PSI

---

## 1. Tóm tắt nhanh

CKA, viết tắt của **Certified Kubernetes Administrator**, là chứng chỉ Kubernetes dành cho người làm quản trị cụm Kubernetes. Bài thi **KHÔNG** phải trắc nghiệm, mà là bài thi **online, remote proctored, performance-based**, tức là học viên phải xử lý các bài thực hành trực tiếp trên terminal.

Tính đến thời điểm cập nhật tài liệu này, bài thi CKA có các thông số chính sau:

| Hạng mục | Thông tin |
|---|---|
| Tên chứng chỉ | Certified Kubernetes Administrator |
| Đơn vị | CNCF + The Linux Foundation |
| Hình thức thi | Online, remote proctored, performance-based |
| Nền tảng giám sát | PSI Bridge / PSI Secure Browser |
| Thời lượng | 2 giờ |
| Số lượng task | Khoảng 15–20 task thực hành |
| Điểm đậu | 66% trở lên |
| Kết quả | Thường có trong vòng 24 giờ sau khi hoàn tất bài thi |
| Kubernetes version hiện tại | Kubernetes v1.35 |
| Ngôn ngữ đề | English, Simplified Chinese, Japanese |
| Giá niêm yết exam only | 445 USD |
| Thời hạn thi sau khi mua | 12 tháng |
| Retake | 1 retake nếu đủ điều kiện |
| Hiệu lực chứng chỉ | 2 năm |
| Simulator | Thường có Killer.sh simulator, nhưng không áp dụng với một số gói SINGLE |

Để học viên dễ hình dung:

> “CKA không hỏi học viên Pod là gì theo kiểu trắc nghiệm. CKA đưa học viên vào terminal và bắt học viên làm cho cluster Kubernetes chạy đúng. Học viên phải biết dùng `kubectl`, đọc log, đọc event, sửa YAML, troubleshoot node/control plane/network/storage và thao tác đủ nhanh trong 2 giờ.”

---

## 2. CKA là chứng chỉ gì?

CKA là chứng chỉ được tạo bởi **The Linux Foundation** và **Cloud Native Computing Foundation (CNCF)**. Mục tiêu là xác nhận người đạt chứng chỉ có kỹ năng, kiến thức và năng lực để thực hiện trách nhiệm của một Kubernetes Administrator.

CKA phù hợp với các nhóm sau:

- Kubernetes Administrator.
- Cloud Engineer / Cloud Architect làm việc với Kubernetes.
- DevOps Engineer / Platform Engineer.
- System Engineer đang chuyển sang Cloud Native.
- Giảng viên Kubernetes muốn có chứng chỉ vendor-neutral.
- Đội vận hành private cloud / managed Kubernetes / container platform.

CKA có tính vendor-neutral, nghĩa là không gắn riêng với AWS EKS, Azure AKS, Google GKE, OpenShift hay một bản phân phối Kubernetes cụ thể nào. Bài thi tập trung vào năng lực Kubernetes lõi: vận hành cluster, workload, networking, storage, RBAC, kubeadm, troubleshooting.

---

## 3. Bản chất bài thi: performance-based, không phải trắc nghiệm

CKA là bài thi thực hành. Học viên sẽ được đưa vào một môi trường thi có sẵn terminal, Kubernetes cluster/node và đề bài ở giao diện Exam UI.

Ví dụ dạng task có thể gặp:

- Tạo Deployment với số replica cụ thể.
- Expose ứng dụng bằng Service.
- Tạo hoặc sửa NetworkPolicy.
- Tạo PersistentVolume/PersistentVolumeClaim.
- Cấu hình StorageClass.
- Backup/restore etcd.
- Upgrade cluster bằng kubeadm.
- Sửa kubelet hoặc static pod bị lỗi.
- Troubleshoot Pod Pending, CrashLoopBackOff, ImagePullBackOff.
- Sửa Service selector sai khiến endpoint rỗng.
- Kiểm tra log container.
- Cấu hình RBAC Role/RoleBinding.
- Cấu hình node affinity, taints, tolerations.
- Làm việc với Ingress/Gateway API.

Điều này có nghĩa là học viên không thể chỉ học lý thuyết. Phải luyện thao tác thật, càng nhiều càng tốt.

---

## 4. Kubernetes version tháng 6/2026

Theo FAQ và trang CKA hiện tại của Linux Foundation, môi trường CKA đang chạy **Kubernetes v1.35**. Linux Foundation cũng ghi rằng môi trường thi sẽ được align theo Kubernetes minor version mới nhất trong khoảng **4–8 tuần** sau khi Kubernetes release.

Vì vậy, nếu thi batch tháng 6/2026, nên training theo Kubernetes **v1.35**.

---

## 5. Cấu trúc nội dung thi CKA

CKA hiện chia thành 5 domain chính:

| Domain | Trọng số | Nội dung chính |
|---|---:|---|
| Troubleshooting | 30% | Troubleshoot clusters/nodes, cluster components, resource usage, container output streams, services/networking |
| Cluster Architecture, Installation & Configuration | 25% | RBAC, hạ tầng cài cluster, kubeadm, cluster lifecycle, HA control plane, Helm/Kustomize, CNI/CSI/CRI, CRD/Operator |
| Services & Networking | 20% | Pod connectivity, NetworkPolicy, Service types, endpoints, Gateway API, Ingress, CoreDNS |
| Workloads & Scheduling | 15% | Deployment, rolling update/rollback, ConfigMap/Secret, autoscaling, self-healing workloads, admission/scheduling/limits/node affinity |
| Storage | 10% | StorageClass, dynamic provisioning, volume types, access modes, reclaim policy, PV/PVC |



Học viên cần quen các thao tác:

```bash
kubectl get
kubectl describe
kubectl logs
kubectl exec
kubectl get events
systemctl status kubelet
journalctl -u kubelet
crictl ps
crictl logs
```

---

## 6. Môi trường thi thực tế

Bài thi diễn ra online qua nền tảng PSI Bridge và PSI Secure Browser. Học viên dùng máy cá nhân để kết nối vào môi trường thi từ xa. Bên trong môi trường thi có:

- Exam UI hiển thị task.
- Terminal.
- Browser để truy cập tài liệu được phép.
- Một hoặc nhiều host/cluster Kubernetes đã được chuẩn bị.

Linux Foundation hướng dẫn rằng mỗi task sẽ chỉ định một host cụ thể. Học viên cần SSH vào host đó để làm bài:

```bash
ssh <nodename>
```

Sau khi làm xong task, học viên nên thoát khỏi SSH session:

```bash
exit
```

Không nên tạo nested SSH session vì môi trường thi không support tốt kiểu này.

### Lưu ý cực quan trọng

Học viên phải đọc kỹ từng task về:

- Cluster/context cần làm.
- Host cần SSH.
- Namespace.
- Tên resource.
- Yêu cầu output.
- Có cần lưu file YAML vào path cụ thể hay không.
- Có cần preserve existing config hay không.

Một lỗi rất phổ biến là làm đúng kỹ thuật nhưng sai namespace hoặc sai context. Trường hợp này vẫn mất điểm.

---

## 7. Công cụ có sẵn trong môi trường thi

Trên các SSH host của exam, thường có sẵn một số công cụ:

- `kubectl`
- Alias `k`
- Bash autocompletion
- `yq`
- `curl`
- `wget`
- `man`
- Man pages
- Một số công cụ Linux cơ bản

Tuy nhiên, base system không nhất thiết có đầy đủ tool. Học viên phải thao tác trên host được đề yêu cầu.

### Khuyến nghị cho lớp học

Học viên nên tập dùng alias:

```bash
alias k=kubectl
complete -o default -F __start_kubectl k
```

Và luyện thao tác với `--dry-run=client -o yaml`:

```bash
kubectl create deployment nginx --image=nginx --replicas=3 --dry-run=client -o yaml > deploy.yaml
```

---

## 8. Được dùng tài liệu gì khi thi?

CKA không phải closed-book tuyệt đối. Học viên được dùng một số tài liệu chính thức trong môi trường thi, nhưng không được dùng Google hay tài liệu cá nhân.

Các tài liệu được phép gồm:

| Resource | Ghi chú |
|---|---|
| Kubernetes Documentation | Được dùng browser trong VM để truy cập |
| Kubernetes Blog | Được phép |
| Helm Documentation | Được phép |
| Task-specific documentation trong Quick Reference box | Được phép |
| Gateway API Documentation | Chỉ áp dụng cho CKA |
| Documents trong distribution, ví dụ `/usr/share` | Được phép |
| Packages thuộc distribution | Có thể dùng/cài nếu phù hợp |

### Không được dùng

- Google search ngoài phạm vi Kubernetes docs.
- ChatGPT hoặc AI assistant.
- Notes cá nhân.
- Bookmark cá nhân.
- Course manual.
- Blog ngoài.
- GitHub cá nhân.
- StackOverflow.
- File nháp đã chuẩn bị sẵn.
- Email/chat/text-based client.

### Cách học viên dùng docs

1. Câu đơn giản: làm bằng trí nhớ và imperative command.
2. Câu YAML dài: dùng docs để copy skeleton.
3. Câu troubleshoot: ưu tiên `describe`, `logs`, `events`, `systemctl`, `journalctl`.
4. Câu không chắc field YAML: dùng `kubectl explain`.

Ví dụ:

```bash
kubectl explain deployment.spec.template.spec.containers
kubectl explain networkpolicy.spec.ingress
kubectl explain pod.spec.affinity
```

---

## 9. Yêu cầu máy tính, phòng thi, camera

Học viên cần chuẩn bị nghiêm túc vì PSI Secure Browser và proctoring khá chặt.

### Yêu cầu chính

| Nhóm | Quy định/lưu ý |
|---|---|
| Máy tính | Dùng máy cá nhân, không khuyến nghị máy công ty |
| OS | Phải nằm trong danh sách PSI support |
| Browser | Chrome được khuyến nghị vì Secure Browser dựa trên Chrome |
| Monitor | Chỉ được dùng 1 monitor; dual monitor không được support |
| Màn hình | Khuyến nghị 15 inch trở lên, 1080p |
| Internet | Ưu tiên mạng dây; tắt sync/Dropbox/BitTorrent/streaming |
| Microphone | Phải hoạt động |
| Webcam | Phải xoay được để scan phòng |
| VM | Không được thi bằng virtual machine |
| Antivirus/firewall | Nên tắt hoặc dùng máy cá nhân không bị policy công ty |
| Nguồn điện | Laptop nên cắm sạc |
| Phòng thi | Riêng tư, yên tĩnh, đủ sáng |
| Bàn thi | Không giấy, bút, điện thoại, thiết bị điện tử |

### Với học viên dùng Mac

Cần kiểm tra trước quyền cho PSI Secure Browser:

- Microphone.
- Camera.
- Automation.
- Input Monitoring.
- Screen Recording nếu được yêu cầu.

Nên reboot máy trước giờ thi và đóng toàn bộ ứng dụng không cần thiết.

---

## 10. Yêu cầu giấy tờ tùy thân

Học viên cần giấy tờ tùy thân hợp lệ:

- Là giấy tờ chính phủ cấp.
- Còn hạn.
- Bản gốc, không phải bản photo hay ảnh chụp.
- Có tên, ảnh và chữ ký.
- Tên trên ID phải khớp với tên đã verify trong exam checklist.

Các loại ID thường được chấp nhận:

- Passport.
- Căn cước công dân / national identity card.
- Driver’s license.
- Giấy tờ chính phủ có ảnh và chữ ký.

Lưu ý cho học viên Việt Nam: nên dùng CCCD hoặc passport còn hạn, và kiểm tra tên trên Linux Foundation account trước khi thi.

---

## 11. Scheduling, reschedule và retake

Sau khi mua exam, học viên thường có **12 tháng** để schedule và thi.

### Reschedule/cancel

Học viên có thể reschedule/cancel nếu còn hơn 24 giờ trước giờ thi. Nếu sát hơn 24 giờ, thường không đổi được và có thể mất lượt thi.

### Retake

CKA thường có 1 retake nếu eligible. Tuy nhiên:

- Retake chỉ có sau khi attempt đầu bị No Pass.
- Phải còn trong thời hạn eligibility.
- Không nên thi attempt đầu quá sát ngày hết hạn.
- Nên để dư ít nhất 1–2 tuần để còn xử lý retake nếu cần.

Không nên để gần hết 12 tháng mới thi. Nếu mua exam rồi, nên lên kế hoạch:

- Học/lab 4–8 tuần.
- Thi thử.
- Schedule exam.
- Chừa buffer cho retake.

---

## 12. Killer.sh simulator

Khi đăng ký CKA, học viên thường có quyền truy cập exam simulator của Killer.sh. Tuy nhiên cần kiểm tra đúng gói mua, vì một số gói `CKA-SINGLE` có thể không bao gồm simulator.

Thông tin phổ biến:

- Có 2 simulation attempts.
- Mỗi attempt mở trong 36 giờ từ lúc activate.
- CKA simulator có bộ câu thực hành mô phỏng môi trường thi.
- Killer.sh thường khó hơn thi thật, nhưng rất tốt để luyện tốc độ và áp lực.

### Khi nào nên activate Killer.sh?

Không nên activate ngay lúc mới học. Nên dùng khi học viên đã:

- Nắm kubectl cơ bản.
- Làm được Deployment/Service/ConfigMap/Secret/PV/PVC.
- Biết troubleshoot Pod/Service/Node cơ bản.
- Đã học qua kubeadm, etcd, RBAC, NetworkPolicy.
- Đã làm lab ít nhất 70–80% nội dung CKA.

---

## 13. Chiến lược học CKA cho học viên

CKA nên học theo hướng **lab-first**.

Tỷ lệ khuyến nghị:

- 20–30% lý thuyết.
- 70–80% lab.

### Giai đoạn 1: Kubernetes core và kubectl speed

Học viên cần rất quen:

```bash
kubectl get
kubectl describe
kubectl logs
kubectl exec
kubectl apply -f
kubectl create
kubectl expose
kubectl scale
kubectl rollout status
kubectl rollout undo
kubectl explain
kubectl auth can-i
```

Cần dùng thành thạo:

```bash
-n
-A
-o wide
-o yaml
--dry-run=client -o yaml
--context
--kubeconfig
```

Ví dụ:

```bash
kubectl create deployment nginx --image=nginx --replicas=3 --dry-run=client -o yaml > deploy.yaml
kubectl expose deployment nginx --port=80 --target-port=80 --type=ClusterIP
kubectl get svc
kubectl get endpoints
```

---

## 14. Cluster Architecture, Installation & Configuration

Domain này chiếm 25%, gồm nhiều phần quan trọng.

### RBAC

Ví dụ tạo ServiceAccount, Role, RoleBinding:

```bash
kubectl create namespace dev
kubectl create serviceaccount app-sa -n dev
kubectl create role pod-reader --verb=get,list,watch --resource=pods -n dev
kubectl create rolebinding read-pods --role=pod-reader --serviceaccount=dev:app-sa -n dev
kubectl auth can-i list pods --as=system:serviceaccount:dev:app-sa -n dev
```

### kubeadm

Cần hiểu:

```bash
kubeadm init
kubeadm join
kubeadm upgrade plan
kubeadm upgrade apply
```

Cần biết thao tác package:

```bash
apt-mark unhold kubeadm kubelet kubectl
apt-get update
apt-get install -y kubeadm=<version>
apt-mark hold kubeadm kubelet kubectl
systemctl daemon-reload
systemctl restart kubelet
```

### Static pods

Manifest thường nằm ở:

```bash
/etc/kubernetes/manifests/
```

Ví dụ:

```bash
ls -l /etc/kubernetes/manifests/
cat /etc/kubernetes/manifests/kube-apiserver.yaml
```

### etcd backup/restore

Backup snapshot:

```bash
ETCDCTL_API=3 etcdctl snapshot save /backup/etcd.db \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key
```

Verify snapshot:

```bash
ETCDCTL_API=3 etcdctl snapshot status /backup/etcd.db --write-out=table
```

Restore snapshot cần rất cẩn thận với path data-dir và static pod manifest.

---

## 15. Workloads & Scheduling

Domain này chiếm 15%.

### Deployment rolling update/rollback

```bash
kubectl create deployment web --image=nginx:1.26 --replicas=3
kubectl set image deployment/web nginx=nginx:1.27
kubectl rollout status deployment/web
kubectl rollout history deployment/web
kubectl rollout undo deployment/web
```

### ConfigMap và Secret

```bash
kubectl create configmap app-config --from-literal=MODE=prod
kubectl create secret generic db-secret --from-literal=password='SuperSecret'
```

Mount vào Pod qua env:

```yaml
env:
- name: MODE
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: MODE
```

### Scheduling

Cần nắm:

- `nodeSelector`
- `nodeAffinity`
- `podAffinity`
- `podAntiAffinity`
- `taints`
- `tolerations`
- resource `requests`
- resource `limits`

Debug Pod Pending:

```bash
kubectl describe pod <pod> -n <namespace>
kubectl get events -n <namespace> --sort-by=.metadata.creationTimestamp
```

Lý do Pending thường gặp:

- Không đủ CPU/RAM.
- Node bị taint nhưng Pod không có toleration.
- `nodeSelector` sai.
- PVC chưa bound.
- Admission/scheduling rule không phù hợp.

---

## 16. Services & Networking

Domain này chiếm 20%.

### Service

Cần nắm các loại:

- ClusterIP.
- NodePort.
- LoadBalancer.
- Headless Service.
- Endpoints / EndpointSlices.

Ví dụ:

```bash
kubectl expose deployment web --port=80 --target-port=8080 --type=ClusterIP
kubectl get svc web
kubectl get endpoints web
kubectl describe svc web
```

Nếu Service không route được, kiểm tra:

```bash
kubectl get pods --show-labels
kubectl get svc <svc> -o yaml
kubectl get endpoints <svc>
```

Bẫy phổ biến: selector của Service không match label của Pod.

### DNS/CoreDNS

Test DNS bằng Pod tạm:

```bash
kubectl run tmp --image=busybox:1.36 -it --rm --restart=Never -- sh
nslookup kubernetes.default.svc.cluster.local
nslookup <service>.<namespace>.svc.cluster.local
```

Kiểm tra CoreDNS:

```bash
kubectl get pods -n kube-system -l k8s-app=kube-dns
kubectl logs -n kube-system -l k8s-app=kube-dns
```

### NetworkPolicy

Cần hiểu:

- Mặc định Kubernetes cho phép traffic nếu không có NetworkPolicy select Pod.
- Khi Pod bị select bởi NetworkPolicy, traffic sẽ bị giới hạn theo rule.
- Ingress và egress độc lập nhau.
- Cần label namespace/pod đúng.

Ví dụ skeleton:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-from-frontend
  namespace: app
spec:
  podSelector:
    matchLabels:
      role: backend
  policyTypes:
  - Ingress
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
    ports:
    - protocol: TCP
      port: 8080
```

### Ingress và Gateway API

CKA hiện có Gateway API trong curriculum. Học viên nên biết cơ bản:

- GatewayClass.
- Gateway.
- HTTPRoute.
- listener.
- parentRefs.
- backendRefs.

Ví dụ các resource hay gặp:

```yaml
kind: GatewayClass
kind: Gateway
kind: HTTPRoute
```

Không nhất thiết học quá sâu như production API Gateway, nhưng cần đọc được YAML và biết route traffic cơ bản.

---

## 17. Storage

Domain này chiếm 10%.

Cần nắm:

- StorageClass.
- PersistentVolume.
- PersistentVolumeClaim.
- Dynamic provisioning.
- Access modes: RWO, ROX, RWX.
- Reclaim policy: Retain, Delete.
- Volume types.
- PVC binding.

Các lệnh cần quen:

```bash
kubectl get sc
kubectl get pv
kubectl get pvc -A
kubectl describe pvc <pvc> -n <namespace>
kubectl describe pv <pv>
```

Ví dụ PVC:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: data-pvc
spec:
  accessModes:
  - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: standard
```

Mount PVC vào Pod:

```yaml
volumes:
- name: data
  persistentVolumeClaim:
    claimName: data-pvc
containers:
- name: app
  image: nginx
  volumeMounts:
  - name: data
    mountPath: /usr/share/nginx/html
```

Lỗi hay gặp:

- PVC Pending do không có StorageClass.
- StorageClass name sai.
- PV capacity nhỏ hơn PVC request.
- Access mode không match.
- Reclaim policy làm dữ liệu bị xóa ngoài ý muốn.

---

## 18. Troubleshooting – phần quan trọng nhất

Troubleshooting chiếm 30%, là domain nặng nhất.

### Bộ lệnh phản xạ

```bash
kubectl get nodes
kubectl describe node <node>
kubectl get pods -A -o wide
kubectl describe pod <pod> -n <namespace>
kubectl logs <pod> -n <namespace>
kubectl logs <pod> -c <container> -n <namespace>
kubectl get events -A --sort-by=.metadata.creationTimestamp
systemctl status kubelet
journalctl -u kubelet
crictl ps
crictl logs <container-id>
```

### Pod troubleshoot

Các trạng thái hay gặp:

- Pending.
- CrashLoopBackOff.
- ImagePullBackOff.
- ErrImagePull.
- CreateContainerConfigError.
- RunContainerError.
- Completed nhưng không đúng yêu cầu.
- Running nhưng readiness probe fail.

Cách xử lý:

```bash
kubectl describe pod <pod> -n <ns>
kubectl logs <pod> -n <ns>
kubectl logs <pod> -c <container> -n <ns>
kubectl get events -n <ns> --sort-by=.metadata.creationTimestamp
```

### Node troubleshoot

```bash
kubectl get nodes
kubectl describe node <node>
ssh <node>
systemctl status kubelet
journalctl -u kubelet -n 100
```

Lỗi hay gặp:

- kubelet stopped.
- kubelet config sai.
- certificate/path sai.
- container runtime lỗi.
- disk pressure/memory pressure.
- node bị cordon/taint.
- static pod manifest lỗi.

### Control plane troubleshoot

Kiểm tra static pod:

```bash
ls -l /etc/kubernetes/manifests/
cat /etc/kubernetes/manifests/kube-apiserver.yaml
cat /etc/kubernetes/manifests/kube-controller-manager.yaml
cat /etc/kubernetes/manifests/kube-scheduler.yaml
cat /etc/kubernetes/manifests/etcd.yaml
```

Kiểm tra container runtime:

```bash
crictl ps -a
crictl logs <container-id>
```

---

## 19. Các bẫy học viên hay dính

### Bẫy 1: Sai namespace

Ví dụ đề yêu cầu namespace `prod`, nhưng học viên tạo resource ở `default`.

Cách tránh:

```bash
kubectl get ns
kubectl config set-context --current --namespace=<namespace>
```

Hoặc luôn dùng `-n`:

```bash
kubectl get pods -n prod
```

### Bẫy 2: Sai context/cluster

Cách kiểm tra:

```bash
kubectl config get-contexts
kubectl config current-context
```

Nếu đề yêu cầu switch context:

```bash
kubectl config use-context <context-name>
```

### Bẫy 3: Viết YAML từ đầu quá lâu

Nên generate skeleton:

```bash
kubectl create deployment app --image=nginx --dry-run=client -o yaml > app.yaml
```

Sau đó sửa file.

### Bẫy 4: Không biết bỏ qua câu khó

Nếu một câu troubleshoot mất quá lâu, nên ghi lại số câu rồi chuyển câu khác. Đừng để một task ăn 30 phút.

### Bẫy 5: Dùng docs quá nhiều

Được dùng docs không có nghĩa là có thời gian đọc docs. Cần biết trước vị trí các YAML mẫu thường dùng.

### Bẫy 6: Không verify sau khi làm

Sau khi tạo/sửa resource, nên kiểm tra lại:

```bash
kubectl get
kubectl describe
kubectl logs
kubectl get events
```

---

## 20. Checklist trước ngày thi

### Trước ngày thi 7 ngày

- Kiểm tra Linux Foundation account.
- Kiểm tra tên trùng với ID.
- Kiểm tra exam eligibility.
- Schedule exam.
- Làm PSI system check.
- Làm ít nhất một mock exam.
- Chạy thử môi trường một màn hình.

### Trước ngày thi 3 ngày

- Reboot máy test.
- Kiểm tra webcam/mic.
- Kiểm tra mạng.
- Kiểm tra quyền camera/mic nếu dùng Mac.
- Dọn phòng thi.
- Chuẩn bị CCCD/passport.
- Hoàn tất Killer.sh nếu có.

### Trước giờ thi 1–2 giờ

- Ăn uống nhẹ.
- Đi vệ sinh trước.
- Cắm sạc laptop.
- Tắt app sync, chat, email, meeting.
- Tắt màn hình phụ.
- Dọn sạch bàn.
- Đặt điện thoại xa khỏi bàn.
- Reboot máy nếu cần.
- Vào sớm hơn giờ thi.

---

## 21. Lộ trình ôn tập đề xuất

### Lộ trình 4–6 tuần cho học viên đã có nền Kubernetes

| Tuần | Nội dung |
|---|---|
| Tuần 1 | kubectl, Pod, Deployment, ReplicaSet, namespace, label/selector, rollout, logs, exec |
| Tuần 2 | Service, DNS, CoreDNS, Ingress, Gateway API, NetworkPolicy |
| Tuần 3 | StorageClass, PV/PVC, volume, ConfigMap, Secret, scheduling, taint/toleration, affinity |
| Tuần 4 | kubeadm, cluster upgrade, RBAC, Helm/Kustomize, CRD/Operator concept, etcd backup/restore |
| Tuần 5 | Troubleshooting node/control plane/network/storage/workload |
| Tuần 6 | Mock exam, Killer.sh, luyện tốc độ, luyện docs navigation, chiến thuật thi |

### Lộ trình 8–10 tuần cho học viên mới

| Giai đoạn | Nội dung |
|---|---|
| Tuần 1–2 | Linux/container/Kubernetes fundamentals |
| Tuần 3–4 | Workloads, Service, ConfigMap, Secret |
| Tuần 5 | Storage và scheduling |
| Tuần 6 | Cluster installation, kubeadm, RBAC |
| Tuần 7 | Networking, Ingress, Gateway API, NetworkPolicy |
| Tuần 8 | Troubleshooting tổng hợp |
| Tuần 9 | Mock exam và sửa điểm yếu |
| Tuần 10 | Final review và thi |

---

## 22. Bộ lab tối thiểu nên có cho CKA

Nên chuẩn bị ít nhất:

1. Lab tạo namespace, Pod, Deployment.
2. Lab scale/rollout/rollback Deployment.
3. Lab ConfigMap/Secret inject vào Pod.
4. Lab Service ClusterIP/NodePort.
5. Lab Service selector sai và sửa endpoint.
6. Lab CoreDNS lookup.
7. Lab NetworkPolicy allow/deny.
8. Lab PV/PVC/StorageClass.
9. Lab nodeSelector/affinity.
10. Lab taint/toleration.
11. Lab RBAC Role/RoleBinding.
12. Lab kubeadm init/join.
13. Lab kubeadm upgrade.
14. Lab etcd snapshot backup/restore.
15. Lab static pod manifest lỗi.
16. Lab kubelet stopped.
17. Lab Pod CrashLoopBackOff.
18. Lab ImagePullBackOff.
19. Lab PVC Pending.
20. Lab Ingress/Gateway API cơ bản.

---

## 23. Nguồn tham khảo chính thức

1. CNCF – Certified Kubernetes Administrator (CKA)  
   https://www.cncf.io/training/certification/cka/

2. The Linux Foundation – Certified Kubernetes Administrator (CKA)  
   https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka/

3. The Linux Foundation – CKA-JP page, có thông tin Kubernetes v1.35, curriculum, giá, retake, simulator  
   https://training.linuxfoundation.org/certification/certified-kubernetes-administrator-cka-jp/

4. Linux Foundation Docs – Frequently Asked Questions: CKA and CKAD & CKS  
   https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks

5. Linux Foundation Docs – Important Instructions: CKA and CKAD  
   https://docs.linuxfoundation.org/tc-docs/certification/tips-cka-and-ckad

6. Linux Foundation Docs – Resources Allowed: All LF Certification Programs  
   https://docs.linuxfoundation.org/tc-docs/certification/certification-resources-allowed

7. Linux Foundation Docs – Candidate Requirements  
   https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/candidate-requirements

8. Linux Foundation Docs – Exam Preparation Checklist  
   https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/exam-preparation-checklist

9. Linux Foundation Docs – Taking the Exam  
   https://docs.linuxfoundation.org/tc-docs/certification/lf-handbook2/taking-the-exam

10. Gateway API Documentation  
    https://gateway-api.sigs.k8s.io/

11. Kubernetes Documentation  
    https://kubernetes.io/docs/

12. Helm Documentation  
    https://helm.sh/docs/
