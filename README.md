
# Giới thiệu
Game N - Puzzle là trò chơi cổ điển với nhiều phiên bản và tên gọi khác như : 8 - Puzzle, 15 - Puzzle, ...
Bài toán N - Puzzle là một trong những bài toán điển hình mô phỏng cho các giải thuật tìm kiếm liên quan đến trí tuệ nhân tạo.

- Trạng thái: mỗi trạng thái là một sắp xếp cụ thể vị trí các ô
- Hành động: mỗi hành động tương ứng với một di chuyển ô trống trái, phải, lên, xuống
- Trạng thái xuất phát: được cho trước 
- Trạng thái đích: được cho một cách tường minh
- Giá thành: bằng tổng số lần dịch chuyển ô trống. Nói cách khác, mỗi chuyển động có giá thành bằng 1.
Lời giải là chuỗi các hành động cho phép di chuyển từ trạng thái xuất phát tới đích. Lời giải cần ít hành động hơn là lời giải tốt hơn.

# 1. Mục tiêu
- Triển khai các thuật toán tìm kiếm bao gồm: tìm kiếm không thông tin (uninformed), tìm kiếm có thông tin (informed), tìm kiếm cục bộ (local search), tìm kiếm phi quyết định (non-deterministic), bài toán thỏa mãn ràng buộc (constraint satisfaction), học tăng cường (reinforcement learning), cùng với tìm kiếm trong môi trường phức tạp, nhằm giải quyết bài toán 8-puzzle. Mục tiêu giúp người dùng hiểu sâu sắc cơ chế hoạt động cũng như hiệu suất của từng thuật toán.

- Thực hiện phân tích và so sánh chi tiết hiệu quả của các thuật toán dựa trên các tiêu chí như thời gian thực thi, mức sử dụng bộ nhớ, và độ tối ưu của đường đi tìm được qua đó làm nổi bật ưu điểm và hạn chế của từng thuật toán.

- Ngoài ra cung cấp giao diện đồ họa trực quan (GUI) hỗ trợ người dùng dễ dàng theo dõi quá trình giải bài toán 8-puzzle một cách sinh động và trực quan nhất.

# 2. Các thuật toán tìm kiếm

## 2.1. Uniformed Search
Tìm kiếm không có thông tin, còn gọi là tìm kiếm mù (blind, uninformed search) là phương pháp duyệt không gian trạng thái chỉ sử dụng các thông tin theo phát biểu của bài toán tìm kiếm tổng quát trong quá trình tìm kiếm, ngoài ra không sử dụng thêm thông
tin nào khác.

- State Space: Mỗi trạng thái là một cấu hình hợp lệ của bảng 8-puzzle, gồm 8 ô số từ 1 đến 8 và 1 ô trống (ký hiệu là 0).
Tổng số trạng thái hợp lệ là **9! = 362,880**, nhưng chỉ một nửa trong số đó là khả thi (do tính chất hoán vị chẵn/lẻ).
- Initial State: Là cấu hình ban đầu của 9 ô được cung cấp.
- Operators / Actions: Các hành động di chuyển ô trống (0) theo 4 hướng: Trái (Left), Phải (Right), Lên (Up), Xuống (Down). Chỉ hợp lệ nếu không vượt khỏi biên của bảng 3x3.
- Transition Model: Sau khi thực hiện một hành động hợp lệ, ô sẽ chuyển sang trạng thái mới bằng cách hoán đổi ô trống với ô kề bên theo hướng di chuyển.
- Goal State: Là trạng thái sắp xếp đúng thứ tự mà chúng ta muốn 
- Đối với tìm kiếm không thông tin như BFS, DFS, UCS, mỗi hành động thường có chi phí bằng nhau
-> chi phí tổng thường là số bước từ trạng thái ban đầu đến trạng thái đích.
- Solution: Là một danh sách cách trạng thái biểu diễn đường đi từ trạng thái khởi đầu đến trạng thái mục tiêu

### BFS (Breadth-First Search) – tìm theo bề rộng.
- BrFS xem các trạng thái như là các đỉnh của một đồ thị cây với mỗi đỉnh con sẽ là trạng thái kế tiếp của đỉnh cha.
- *Bước thực hiện:*
    1. Bắt đầu từ trạng thái ban đầu, đưa nó vào hàng đợi (queue).
    2. Đánh dấu trạng thái đã được duyệt (visited/closed).
    3. Lặp lại đến khi hàng đợi rỗng:
        - Lấy trạng thái hiện tại từ hàng đợi.
        - Nếu như trạng thái hiện tại chính là trạng thái đích:
            - Trả về các bước đến trạng thái hiện tại
        - Duyệt từng trạng thái sinh ra từ trạng thái hiện tại:
            - Nếu trạng thái là *hợp lệ* và *chưa được duyệt*
                - Đánh dấu trạng thái đã được duyệt (đưa vào visited/closed)
                - Đưa vào hàng đợi.
    4. Trả về null nếu như không có lời giải.
### DFS (Depth-First Search) – tìm theo chiều sâu
- Giống như BrFS, DFS cũng coi các trạng thái như một đồ thị cây. Điểm khác biệt của DFS so với BrFS là thuật giải này sẽ duyệt hết các trạng thái có thể của một nhánh thay vì duyệt từng lớp của các nhánh.
- *Bước thực hiện:*
    1. Bắt đầu từ trạng thái ban đầu, đưa nó vào ngăn xếp (stack).
    2. Đánh dấu trạng thái đã được duyệt.
    3. Lặp lại đến khi ngăn xếp rỗng:
        - Lấy trạng thái hiện tại từ ngăn xếp.
        - Nếu đường đi hiện tại vượt quá độ sâu tuyệt đối:
            - Bỏ qua trạng thái này.
        - Nếu như trạng thái hiện tại chính là trạng thái đích:
            - Trả về các bước đến trạng thái hiện tại.
        - Duyệt từng trạng thái sinh ra từ trạng thái hiện tại:
            - Nếu trạng thái là *hợp lệ* và *chưa được duyệt*:
                - Đánh dấu trạng thái đã được duyệt.
                - Đưa vào ngăn xếp.
### UCS (Uniform Cost Search) – ưu tiên trạng thái có chi phí thấp
- UCS giống như BFS nhưng có thêm yếu tố chi phí: nó luôn chọn trạng thái có tổng chi phí thấp nhất để mở rộng trước.
- Trong 8-puzzle, chi phí mỗi bước bằng nhau nên UCS sẽ cho kết quả giống BFS, nhưng UCS vẫn quan trọng khi mỗi bước có chi phí khác nhau.
- Hàm đảm bảo tìm được lời giải có chi phí thấp nhất bằng cách ưu tiên các đường đi rẻ hơn.
- *Bước thực hiện:*
    1. Bắt đầu từ trạng thái ban đầu, đưa nó vào hàng đợi ưu tiên với cost bằng 0.
    2. Đánh dấu trạng thái này đã được duyệt.
    3. Lặp lại đến khi hàng đợi rỗng:
        - Nếu trạng thái hiện tại là trạng thái đích:
            - Trả về các bước đến trạng thái hiện tại.
        - Duyệt qua từng trạng thái con được sinh ra:
            - Cost cho trạng thái đang duyệt tăng 1
            - Nếu như trạng thái chưa từng được duyệt lúc trước hoặc đã được duyệt nhưng có cost thấp hơn:
                - Đưa (cập nhật) trạng thái vào tập hợp các trạng thái đã được duyệt.
                - Thêm trạng thái vào trong hàng đợi.
    4. Trả về rỗng nếu không có câu trả lời. 

### IDS (Iterative Deepening Search) – kết hợp DFS và BFS
Phương pháp: Tìm theo DFS nhưng không bao giờ mở rộng các nút có độ sâu quá một giới hạn nào đó. Giới hạn độ sâu được bắt đầu từ 0, sau đó tăng lên 1, 2, 3 v.v. cho đến khi tìm được lời giải.
- *Bước thực hiện:*
    * Hàm IDS:
        1. Duyệt từng mức độ sâu từ 1 đến max_depth:
            - Gọi hàm DLS với độ sâu depth và trạng thái hiện tại để trả về kết quả.
            - Trả về kết quả
    * Hàm DLS:
        1. Khởi tạo path, visited nếu chúng là null.
        2. Nếu trạng thái hiện tại chưa được duyệt:
            - Đánh dấu là đã được duyệt.
        3. Nếu trạng thái hiện tại là trạng thái đích:
            - Trả về các bước đến trạng thái đích.
        4. Nếu như độ sâu là 0:
            - Trả về null
        5. Duyệt qua các trạng thái tiếp theo được sinh ra:
            - Gọi DLS với các tham số path, visited, và độ sâu giảm đi 1
            - Nếu kết quả khác null:
                - Trả về các bước đến trạng thái hiện tại.
        6. Trả về null nếu không có kết quả. 
### So sánh hiệu suất
BFS sẽ luôn tìm được lời giải nếu tồn tại và lời giải luôn là ngắn nhất. Tiêu tốn bộ nhớ và tài nguyên nếu phải duyệt hết.

DFS nhanh nhưng dễ rơi vào vòng lặp, không đảm bảo lời giải tốt.

UCS tìm đường đi tối ưu nếu chi phí rõ ràng.

IDS tiết kiệm bộ nhớ hơn BFS, nhưng chậm hơn.

## 2.2. Informed Search
Chiến lược tìm kiếm có thông tin (Informed search) hay còn
được gọi là tìm kiếm heuristic sử dụng thêm thông tin từ bài toán để định hướng tìm kiếm, cụ thể là lựa chọn thứ tự mỏ rộng nút theo hướng mau dẫn tới đích hơn Thêm yếu tố Heuristic vào đánh giá trạng thái.
- State Space: 
- Initial State:
- Operators / Actions:
- Transition Model:
- Goal State:
- Solution:
- Evaluation Function: Hàm f(n) = g(n) + h(n) với:
g(n): chi phí từ trạng thái đầu đến trạng thái đang xét

h(n): ước lượng chi phí từ trạng thái đang xét đến trạng thái mục tiêu.
- **Trong bài toán 8-puzzle h(n) sẽ là tổng khoảng cách mahattan của các ô đến vị trí đúng của chúng:**
- ![formula]("https://latex.codecogs.com/svg.image?M(S)=\sum_{i=0}^{N}m(S_{i})")

### Greedy Best-First Search

### A Search*

### IDA (Iterative Deepening A)**

A* là thuật toán hiệu quả nhất, đảm bảo tìm được lời giải tối ưu nếu heuristic phù hợp.

Greedy nhanh nhưng dễ bỏ qua lời giải tối ưu.

IDA* tiết kiệm bộ nhớ nhưng có thể lặp lại nhiều trạng thái

## 2.3. Local Search

### Simple Hill Climbing

### Steepest-Ascent Hill climbing

### Stochastic Hill Climbing

### Simulated Annealing

### Genetic Algorithm

### Beam Search
Giới hạn beam width - lựa chọn 

## 2.4. Search in Complex Environment
Tìm kiếm trong môi trường phức tạp là một lĩnh vực quan trọng trong trí tuệ nhân tạo, nơi các thuật toán phải đối mặt với nhiều yếu tố không chắc chắn và biến động. Môi trường phức tạp có thể bao gồm nhiều trạng thái, các yếu tố tương tác, và các ràng buộc khó khăn, đòi hỏi các phương pháp tìm kiếm phải linh hoạt và hiệu quả.
Đặc điểm của Môi trường Phức tạp
- Nhiều Trạng thái: Môi trường có thể có hàng triệu trạng thái khác nhau, làm cho việc tìm kiếm trở nên khó khăn hơn.
- Tương tác giữa các yếu tố: Các yếu tố trong môi trường có thể tương tác với nhau, ảnh hưởng đến quyết định và kết quả.
- Tính chắc chắn: Thông tin có thể không đầy đủ hoặc không chính xác, yêu cầu các thuật toán phải xử lý sự không chắc chắn này.
- Thay đổi theo thời gian: Môi trường có thể thay đổi theo thời gian, yêu cầu các thuật toán phải thích ứng nhanh chóng.
### 2.4.1. Non Obser
### 2.4.2. Partial Obser
### 2.4.3. AND-OR Search
Thuật toán đầu vào chỉ cần một trạng thái ban đầu.

- Sử dụng mô hình cây AND-OR, trong đó:

- Nút **AND** đại diện cho các trạng thái cần đồng thời đạt được (tất cả con đều phải đúng).

- Nút **OR** đại diện cho các lựa chọn thay thế (chỉ cần một con đúng).

## 2.5. Constraint Satisfaction Problem (CSP)
Bài toán tìm trạng thái thỏa mãn các ràng buộc (khác với tối ưu đường đi).
- **State Space**: Tập các gán giá trị cho biến thỏa mãn tất cả ràng buộc.
- **Initial State**: Biến chưa được gán giá trị.
- **Operators / Actions**: Gán giá trị hợp lệ cho biến theo thứ tự.
Transition Model: Cập nhật các ràng buộc và loại bỏ các giá trị không phù hợp.
- **Goal State**: Gán giá trị đầy đủ cho các biến thỏa mãn mọi ràng buộc.
- **Solution**: Một tập các giá trị biến thỏa mãn toàn bộ ràng buộc.


## 2.6. Reinforcement Learning

- **Agent**: 
- **Environment**: 
- **State**: 
- **Action**: 
- **Reward**: 

