# Game-8-Puzzle

Giới thiệu

8-Puzzle Solver là một ứng dụng Python sử dụng thư viện Pygame để mô phỏng và giải bài toán 8-puzzle (ô số 3x3). Trò chơi bao gồm một bảng 3x3 với 8 ô số (từ 1 đến 8) và một ô trống (0). Mục tiêu là di chuyển ô trống để sắp xếp các ô số từ trạng thái ban đầu về trạng thái đích ([[1, 2, 3], [4, 5, 6], [7, 8, 0]]). Ứng dụng cung cấp nhiều thuật toán tìm kiếm để giải bài toán, từ các phương pháp không sử dụng thông tin (uninformed) đến các phương pháp học tăng cường (reinforcement learning).

Ứng dụng có giao diện đồ họa trực quan, cho phép người dùng:





Chọn thuật toán để giải puzzle.



Tạo bảng ngẫu nhiên có thể giải được.



Di chuyển ô số thủ công bằng chuột hoặc bàn phím.



Xem kết quả về thời gian và số bước của thuật toán.

Yêu cầu hệ thống





Python 3.8 trở lên



Thư viện cần thiết: pygame, asyncio, threading



Cài đặt thư viện:

pip install pygame

Hướng dẫn sử dụng





Cài đặt và chạy:





Tải mã nguồn từ kho lưu trữ.



Chạy tệp main.py:

python main.py



Giao diện:





Bảng puzzle: Hiển thị ở bên trái, với ô trống màu xám và các ô số màu xanh.



Nút điều khiển:





Solve: Chạy thuật toán được chọn để giải puzzle.



Reset: Đặt lại bảng về trạng thái ban đầu.



Random: Tạo bảng ngẫu nhiên có thể giải được.



Lưới thuật toán: Lưới 4x5 ở góc trên phải để chọn thuật toán.



Khu vực kết quả: Hiển thị thời gian và số bước của các thuật toán đã chạy.



Thông báo trạng thái: Hiển thị trạng thái hiện tại (Ready, Solving..., Solved!).



Cách chơi:





Di chuyển thủ công: Nhấn vào ô số liền kề ô trống hoặc sử dụng phím mũi tên (lên, xuống, trái, phải).



Giải tự động: Chọn thuật toán từ lưới và nhấn "Solve" để xem quá trình giải.



Tạo bảng mới: Nhấn "Random" để tạo bảng mới hoặc "Reset" để quay về trạng thái ban đầu.

Các thuật toán giải bài toán 8-Puzzle

Ứng dụng triển khai nhiều thuật toán tìm kiếm, được chia thành các nhóm sau:

1. Tìm kiếm không sử dụng thông tin (Uninformed Search)

Các thuật toán này không sử dụng thông tin heuristic để định hướng tìm kiếm, thay vào đó khám phá tất cả các khả năng một cách có hệ thống.

a. Breadth-First Search (BFS)





Cách hoạt động: Khám phá tất cả các trạng thái ở độ sâu hiện tại trước khi chuyển sang độ sâu tiếp theo. Sử dụng hàng đợi (queue) để lưu trữ các trạng thái.



Ưu điểm: Đảm bảo tìm ra đường đi ngắn nhất (về số bước).



Nhược điểm: Tốn nhiều bộ nhớ do phải lưu trữ tất cả trạng thái ở mỗi độ sâu.



Ứng dụng: Phù hợp khi cần đường đi tối ưu và không gian trạng thái không quá lớn.

b. Depth-First Search (DFS)





Cách hoạt động: Khám phá sâu nhất có thể theo một nhánh trước khi quay lại (backtrack). Sử dụng ngăn xếp (stack) để lưu trữ các trạng thái.



Ưu điểm: Tốn ít bộ nhớ hơn BFS.



Nhược điểm: Không đảm bảo đường đi ngắn nhất, có thể bị kẹt trong nhánh sâu vô hạn nếu không giới hạn độ sâu.



Ứng dụng: Phù hợp khi không gian trạng thái lớn nhưng chấp nhận đường đi không tối ưu.

c. Uniform Cost Search (UCS)





Cách hoạt động: Tương tự BFS nhưng ưu tiên trạng thái có chi phí thấp nhất (số bước). Sử dụng hàng đợi ưu tiên (priority queue).



Ưu điểm: Tìm đường đi tối ưu về chi phí (số bước).



Nhược điểm: Tốn bộ nhớ tương tự BFS.



Ứng dụng: Khi cần tối ưu chi phí trong không gian trạng thái phức tạp.

d. Iterative Deepening Depth-First Search (IDDFS)





Cách hoạt động: Kết hợp ưu điểm của BFS và DFS. Thực hiện DFS với độ sâu giới hạn, tăng dần độ sâu qua từng vòng lặp.



Ưu điểm: Tốn ít bộ nhớ hơn BFS, vẫn đảm bảo đường đi tối ưu.



Nhược điểm: Lặp lại các trạng thái ở các độ sâu thấp, gây tốn thời gian.



Ứng dụng: Phù hợp khi muốn cân bằng giữa bộ nhớ và tính tối ưu.

2. Tìm kiếm sử dụng thông tin (Informed Search)

Các thuật toán này sử dụng heuristic (ví dụ: khoảng cách Manhattan) để ưu tiên khám phá các trạng thái gần với mục tiêu hơn.

a. A*





Cách hoạt động: Kết hợp chi phí thực tế (số bước đã đi) và chi phí ước lượng (heuristic Manhattan) để chọn trạng thái tốt nhất. Sử dụng hàng đợi ưu tiên.



Ưu điểm: Tìm đường đi ngắn nhất với hiệu quả cao hơn BFS/UCS.



Nhược điểm: Vẫn tốn bộ nhớ để lưu trữ các trạng thái đã thăm.



Ứng dụng: Phù hợp khi cần đường đi tối ưu với heuristic tốt.

b. Iterative Deepening A* (IDA*)





Cách hoạt động: Tương tự A* nhưng sử dụng tìm kiếm theo độ sâu với ngưỡng dựa trên tổng chi phí (g + h). Tăng ngưỡng khi không tìm thấy mục tiêu.



Ưu điểm: Tốn ít bộ nhớ hơn A* vì không lưu trữ hàng đợi lớn.



Nhược điểm: Có thể lặp lại các trạng thái, gây tốn thời gian.



Ứng dụng: Phù hợp khi bộ nhớ hạn chế nhưng vẫn cần đường đi tối ưu.

c. Greedy Search





Cách hoạt động: Chỉ sử dụng heuristic (khoảng cách Manhattan) để chọn trạng thái gần mục tiêu nhất, không xem xét chi phí thực tế.



Ưu điểm: Nhanh hơn A* do không tính chi phí thực tế.



Nhược điểm: Không đảm bảo đường đi tối ưu, có thể bị kẹt ở trạng thái không tối ưu.



Ứng dụng: Phù hợp khi cần giải nhanh và chấp nhận đường đi không tối ưu.

3. Tìm kiếm cục bộ (Local Search)

Các thuật toán này tập trung vào cải thiện trạng thái hiện tại thay vì khám phá toàn bộ không gian trạng thái.

a. Genetic Algorithm





Cách hoạt động: Mô phỏng tiến hóa tự nhiên. Tạo một tập hợp trạng thái (population), chọn các trạng thái tốt nhất (dựa trên heuristic), lai ghép (crossover) và đột biến (mutation) để tạo trạng thái mới.



Ưu điểm: Có thể tìm lời giải trong không gian lớn mà không cần khám phá toàn bộ.



Nhược điểm: Không đảm bảo tìm được lời giải, phụ thuộc vào tham số (population size, mutation rate).



Ứng dụng: Phù hợp cho các bài toán phức tạp với không gian trạng thái lớn.

b. Simple Hill Climbing





Cách hoạt động: Chọn trạng thái láng giềng có heuristic tốt nhất (khoảng cách Manhattan thấp hơn) và tiếp tục cho đến khi không còn cải thiện.



Ưu điểm: Đơn giản, nhanh.



Nhược điểm: Dễ bị kẹt ở cực trị cục bộ (local optima).



Ứng dụng: Phù hợp khi cần giải nhanh và chấp nhận kết quả không tối ưu.

c. Steepest-Ascent Hill Climbing





Cách hoạt động: Tương tự Simple Hill Climbing nhưng kiểm tra tất cả láng giềng và chọn trạng thái có heuristic tốt nhất.



Ưu điểm: Hiệu quả hơn Simple Hill Climbing.



Nhược điểm: Vẫn có thể bị kẹt ở cực trị cục bộ.



Ứng dụng: Phù hợp khi cần cải thiện dần trạng thái hiện tại.

d. Stochastic Hill Climbing





Cách hoạt động: Chọn ngẫu nhiên một láng giềng, ưu tiên trạng thái tốt hơn nhưng đôi khi chấp nhận trạng thái tệ hơn để thoát cực trị cục bộ.



Ưu điểm: Giảm nguy cơ kẹt ở cực trị cục bộ.



Nhược điểm: Kết quả không ổn định, phụ thuộc vào yếu tố ngẫu nhiên.



Ứng dụng: Phù hợp khi cần cân bằng giữa khám phá và cải thiện cục!!!!

e. Beam Search





Cách hoạt động: Giữ một tập hợp cố định (beam width) các trạng thái tốt nhất ở mỗi bước, mở rộng các trạng thái này và chọn lại các trạng thái tốt nhất.



Ưu điểm: Hiệu quả hơn BFS trong việc giới hạn không gian tìm kiếm.



Nhược điểm: Có thể bỏ sót lời giải nếu beam width quá nhỏ.



Ứng dụng: Phù hợp khi cần cân bằng giữa hiệu suất và chất lượng lời giải.

f. Simulated Annealing





Cách hoạt động: Chấp nhận các trạng thái tệ hơn với xác suất giảm dần theo thời gian (nhiệt độ), giúp thoát khỏi cực trị cục bộ.



Ưu điểm: Có khả năng tìm lời giải toàn cục.



Nhược điểm: Phụ thuộc vào tham số nhiệt độ và tốc độ làm nguội.



Ứng dụng: Phù hợp khi cần khám phá không gian trạng thái lớn và tránh cực trị cục bộ.

4. Môi trường phức tạp (Complex Environments)

Các thuật toán này xử lý các tình huống với tính không xác định hoặc quan sát hạn chế.

a. AND-OR Graph Search (Tìm kiếm với tính không xác định)





Cách hoạt động: Xử lý các hành động không xác định bằng cách mô phỏng nhiều trạng thái có thể xảy ra cho mỗi hành động. Sử dụng tìm kiếm dựa trên heuristic để ưu tiên nhánh tốt nhất.



Ưu điểm: Xử lý được các tình huống không chắc chắn.



Nhược điểm: Phức tạp, tốn tài nguyên tính toán.



Ứng dụng: Phù hợp khi mô hình hóa các bài toán với hành động không dự đoán được.

b. Belief State Search (Tìm kiếm không quan sát)





Cách hoạt động: Giả định không có thông tin quan sát, duy trì tập hợp các trạng thái có thể (belief states) và tìm kiếm dựa trên chúng. Trong ứng dụng này, được đơn giản hóa thành AND-OR Graph Search.



Ưu điểm: Xử lý được tình huống thiếu thông tin.



Nhược điểm: Tốn tài nguyên do phải theo dõi nhiều trạng thái.



Ứng dụng: Phù hợp cho các bài toán không có quan sát trực tiếp.

c. Partial Observation Search (Tìm kiếm với quan sát một phần)





Cách hoạt động: Tương tự Belief State Search nhưng giả định có một phần thông tin quan sát. Trong ứng dụng này, được đơn giản hóa thành AND-OR Graph Search.



Ưu điểm: Linh hoạt trong môi trường quan sát hạn chế.



Nhược điểm: Phức tạp và tốn tài nguyên.



Ứng dụng: Phù hợp khi chỉ có thông tin một phần về trạng thái.

5. Bài toán thỏa mãn ràng buộc (Constraint Satisfaction Problems - CSPs)

Các thuật toán này xem 8-puzzle như một bài toán CSP, tập trung vào việc giảm xung đột giữa các ô.

a. Backtracking





Cách hoạt động: Thử tất cả các di chuyển có thể, quay lại (backtrack) khi gặp ngõ cụt. Theo dõi các trạng thái đã thăm để tránh lặp.



Ưu điểm: Đơn giản, đảm bảo tìm lời giải nếu tồn tại.



Nhược điểm: Có thể chậm nếu không gian trạng thái lớn.



Ứng dụng: Phù hợp khi cần khám phá có hệ thống.

b. Backtracking with Forward Checking





Cách hoạt động: Tương tự Backtracking nhưng sử dụng kiểm tra trước (forward checking) để loại bỏ các nhánh không khả thi dựa trên heuristic (khoảng cách Manhattan).



Ưu điểm: Hiệu quả hơn Backtracking nhờ cắt tỉa sớm.



Nhược điểm: Vẫn có thể chậm trong trường hợp xấu.



Ứng dụng: Phù hợp khi cần cải thiện hiệu suất của Backtracking.

c. Min-Conflicts





Cách hoạt động: Chọn di chuyển giảm thiểu số ô sai vị trí (conflicts) so với trạng thái đích. Lặp lại cho đến khi đạt mục tiêu.



Ưu điểm: Nhanh, đơn giản.



Nhược điểm: Có thể không tìm được lời giải tối ưu.



Ứng dụng: Phù hợp khi cần giải nhanh dựa trên giảm xung đột cục bộ.

6. Học tăng cường (Reinforcement Learning)

a. Q-Learning





Cách hoạt động: Học chính sách tối ưu bằng cách thử và sai. Cập nhật bảng Q-value dựa trên phần thưởng (đạt mục tiêu: +100, di chuyển: -1) và chọn hành động tốt nhất.



Ưu điểm: Có thể học cách giải mà không cần mô hình rõ ràng.



Nhược điểm: Tốn thời gian huấn luyện, kết quả phụ thuộc vào tham số (số tập, learning rate).



Ứng dụng: Phù hợp khi cần học cách giải trong môi trường động.

Cấu trúc mã nguồn





main.py: Điểm vào của ứng dụng, khởi tạo và chạy trò chơi.



game.py: Chứa lớp PuzzleGUI, quản lý giao diện và tương tác người dùng.



puzzle_state.py: Lớp PuzzleState, biểu diễn trạng thái puzzle và các thao tác (di chuyển, tính heuristic).



search_algorithms.py: Triển khai tất cả các thuật toán tìm kiếm.



utils.py: Các hàm tiện ích như kiểm tra tính giải được (is_solvable) và tạo bảng ngẫu nhiên (generate_solvable_puzzle).

Lưu ý: Để có trải nghiệm tốt nhất, hãy thử các thuật toán khác nhau và so sánh hiệu suất của chúng thông qua khu vực kết quả. Nếu bạn cần thêm thông tin hoặc hỗ trợ, vui lòng liên hệ qua issue trên kho lưu trữ!
