# Logisim
Logisim 개발툴은 http://www.cburch.com/logisim/ 로 진행하였습니다. <br>


ttt 파일은 MIPS의 방식을 채택한 CPU입니다 해당 CPU는 32bit로진행되며 MIPS명령어를 이용한 원사이클 CPU입니다. <br>
# 주의사항
one sycle clock cpu는 한사이클에 IR과 데이터 읽기,쓰기를 동시에 수행할수없으므로, Data와 IR 메모리를 분리하여 한번에 실행되게해야한다 <br>
# CPU회로 설명
1)IFU : Instruction Fetch Unit <br
PC(Program Counter)를 이용하여 명령어 메모리에서 명령어를 읽어온다 IR <- Mem[PC] <br>
일반적인 경우는 PC는 PC+4으로 변화 ,특수경우 BEQ인경우에는 rt와 rs값이 서로 같을경우 PC+4+SignExt(imm16)으로 변경된다. <br>

<br>
1. R타입의 명령어인경우 <br>
  6bit   5bit 5bit 5bit 5bit    6bit  <br>
[opcode] [rt] [rs] [rd] [shamt] [funct] <br>
<br>
ex) ADD경우 <br>
IR <- Mem[PC] <br>
R[rd] <- R[rs] + R[rt] <br>
PC <- PC + 4 <br>
<br>
2. I타입의 경우 <br>
  6bit    5bit 5bit 16bit <br>
[opcode] [rt] [rs] [imm16] <br>
<br>
ex) lw경우 <br>
IR <- Mem[PC] <br>
Addr <- R[rt] + SignExt(imm16) <br>
R[rs] <- Mem[Addr] <br>
PC <- PC + 4  <br>
<br>
ex) beq경우 <br>
IR <- Mem[PC] <br>
Cond <- R[rt] + ~R[rs] + 1  : rt - rs <br>
PC <- Cond ? PC <- PC + 4 <br>
           : PC <- PC + 4 + SignExt(imm16) <br>




