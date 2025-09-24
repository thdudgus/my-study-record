빈칸, 개행, 탭과 같은 비어있지 않은 sequence   
Lexical analyzer는 parsing에 제공하지 않는 흥미롭지 않은 token은 자주 버린다.   
e.g. 스페이스바, 주석   

𝑊ℎ𝑖𝑡𝑒𝑠𝑝𝑎𝑐𝑒 = \\t | \\n | \\t\\t | … → (\\t | \\n)＋
