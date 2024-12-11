
clc;
clear all;
k=input('enter the length of the message word:');
n=input('enter the length of the codeword:');
p=input('enter the parity matrix:');
disp('generator matrix:');
G=[eye(k) p];
disp(G);
m=input('enter the message word:');
disp('codeword:');
C=encode(m,n,k, 'linear',G);
disp(C);
H=[p' eye(n-k)];
disp('h matrix:');
disp(H);
dtable=syndtable(H);
R=input('enter the recieved codeword: ');
Syndrome=rem(R*H', 2);
disp('syndrome:');
disp(Syndrome);
Syn_position=bi2de(Syndrome,'left-msb');
disp('syndrome position:');
disp(Syn_position);
if (Syndrome==0)
 disp('the recieved codeword is valid')
 else
 disp('the recieved codeword is invalid')
 E=dtable(Syn_position+1,:)
 disp('the corrected word is :')
 CC=rem(R+E, 2);
 disp(CC);
 msg=CC(1:k);
end
D=decode(C,n,k,'linear',G);
%[1 1 1 ;1 1 0 ;1 0 1 ;0 1 1 ]
%[0 0 1 1]
%[0 1 1 1 1 1 0]
