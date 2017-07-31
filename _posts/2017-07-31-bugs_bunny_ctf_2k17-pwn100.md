

muffinx@muffinhouse:~/ctf/bugs_bunny_2017/pwn/pwn100$ file pwn100
pwn100: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked, interpreter /lib/ld-linux.so.2, for GNU/Linux 2.6.24, BuildID[sha1]=4eed8d04991f7b37ef1e309f1ecc983d7ff84333, not stripped


gdb-peda$ checksec
CANARY    : disabled
FORTIFY   : disabled
NX        : disabled
PIE       : disabled
RELRO     : Partial



muffinx@muffinhouse:~/ctf/bugs_bunny_2017/pwn/pwn100$ ropgadget --binary pwn100
Gadgets information
============================================================
0x080485bb : adc al, 0x41 ; ret
0x080483bd : add al, 0x24 ; and byte ptr [eax - 0x2d00f7fc], ah ; leave ; ret
0x08048380 : add al, 0x24 ; and byte ptr [eax - 0x2f00f7fc], ah ; leave ; ret
0x080483e8 : add al, 8 ; add ecx, ecx ; ret
0x08048384 : add al, 8 ; call eax
0x080483c1 : add al, 8 ; call edx
0x08048368 : add al, 8 ; cmp eax, 6 ; ja 0x8048377 ; ret
0x0804843c : add byte ptr [eax], al ; add byte ptr [eax], al ; leave ; ret
0x0804843d : add byte ptr [eax], al ; add cl, cl ; ret
0x080482cc : add byte ptr [eax], al ; add esp, 8 ; pop ebx ; ret
0x0804843e : add byte ptr [eax], al ; leave ; ret
0x080485b8 : add cl, byte ptr [eax + 0xe] ; adc al, 0x41 ; ret
0x0804843f : add cl, cl ; ret
0x080485b4 : add eax, 0x2300e4e ; dec eax ; push cs ; adc al, 0x41 ; ret
0x080483e5 : add eax, 0x804a020 ; add ecx, ecx ; ret
0x080483a2 : add eax, edx ; sar eax, 1 ; jne 0x80483af ; ret
0x080483ea : add ecx, ecx ; ret
0x080484a9 : add esp, 0x1c ; pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x080482ce : add esp, 8 ; pop ebx ; ret
0x0804840a : and al, 0x10 ; lahf ; add al, 8 ; call eax
0x08048381 : and al, 0x20 ; mov al, byte ptr [0xd0ff0804] ; leave ; ret
0x080483be : and al, 0x20 ; mov al, byte ptr [0xd2ff0804] ; leave ; ret
0x08048428 : and al, 0xe8 ; ret 0xfffe
0x080483ba : and al, 4 ; mov dword ptr [esp], 0x804a020 ; call edx
0x080483bf : and byte ptr [eax - 0x2d00f7fc], ah ; leave ; ret
0x08048382 : and byte ptr [eax - 0x2f00f7fc], ah ; leave ; ret
0x080483e6 : and byte ptr [eax - 0x36fef7fc], ah ; ret
0x08048366 : and byte ptr [eax - 0x77cf7fc], ah ; push es ; ja 0x8048379 ; ret
0x080482b4 : call 0x8048356
0x0804855b : call dword ptr [ebx]
0x0804857b : call dword ptr [edx]
0x08048386 : call eax
0x080483c3 : call edx
0x080483a5 : clc ; jne 0x80483ac ; ret
0x0804836b : clc ; push es ; ja 0x8048374 ; ret
0x0804836a : cmp eax, 6 ; ja 0x8048375 ; ret
0x080485b9 : dec eax ; push cs ; adc al, 0x41 ; ret
0x0804842d : dec ecx ; ret
0x080485b5 : dec esi ; push cs ; xor byte ptr [edx], al ; dec eax ; push cs ; adc al, 0x41 ; ret
0x080484a8 : fild word ptr [ebx + 0x5e5b1cc4] ; pop edi ; pop ebp ; ret
0x08048421 : in al, dx ; sub byte ptr [ebp + 0x489e845], cl ; and al, 0xe8 ; ret 0xfffe
0x080485bc : inc ecx ; ret
0x0804836d : ja 0x8048372 ; ret
0x080483a6 : jne 0x80483ab ; ret
0x080484a7 : jne 0x8048491 ; add esp, 0x1c ; pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x0804840c : lahf ; add al, 8 ; call eax
0x08048388 : leave ; ret
0x080484aa : les ebx, ptr [ebx + ebx*2] ; pop esi ; pop edi ; pop ebp ; ret
0x080482cf : les ecx, ptr [eax] ; pop ebx ; ret
0x080483e7 : mov al, byte ptr [0xc9010804] ; ret
0x08048383 : mov al, byte ptr [0xd0ff0804] ; leave ; ret
0x080483c0 : mov al, byte ptr [0xd2ff0804] ; leave ; ret
0x08048367 : mov al, byte ptr [0xf8830804] ; push es ; ja 0x8048378 ; ret
0x080483e4 : mov byte ptr [0x804a020], 1 ; leave ; ret
0x08048408 : mov dword ptr [esp], 0x8049f10 ; call eax
0x0804837f : mov dword ptr [esp], 0x804a020 ; call eax
0x080483bc : mov dword ptr [esp], 0x804a020 ; call edx
0x0804843b : mov eax, 0 ; leave ; ret
0x08048350 : mov ebx, dword ptr [esp] ; ret
0x0804834f : nop ; mov ebx, dword ptr [esp] ; ret
0x0804834d : nop ; nop ; mov ebx, dword ptr [esp] ; ret
0x0804834b : nop ; nop ; nop ; mov ebx, dword ptr [esp] ; ret
0x080484b8 : nop ; nop ; nop ; nop ; nop ; nop ; nop ; nop ; ret
0x080484b9 : nop ; nop ; nop ; nop ; nop ; nop ; nop ; ret
0x080484ba : nop ; nop ; nop ; nop ; nop ; nop ; ret
0x080484bb : nop ; nop ; nop ; nop ; nop ; ret
0x080484bc : nop ; nop ; nop ; nop ; ret
0x080484bd : nop ; nop ; nop ; ret
0x080484be : nop ; nop ; ret
0x080484bf : nop ; ret
0x08048385 : or bh, bh ; ror cl, 1 ; ret
0x080483c2 : or bh, bh ; ror cl, cl ; ret
0x08048369 : or byte ptr [ebx + 0x17706f8], al ; ret
0x080483e9 : or byte ptr [ecx], al ; leave ; ret
0x080483a1 : pop ds ; add eax, edx ; sar eax, 1 ; jne 0x80483b0 ; ret
0x080484af : pop ebp ; ret
0x080484ac : pop ebx ; pop esi ; pop edi ; pop ebp ; ret
0x080482d1 : pop ebx ; ret
0x080484ae : pop edi ; pop ebp ; ret
0x080484ad : pop esi ; pop edi ; pop ebp ; ret
0x080485ba : push cs ; adc al, 0x41 ; ret
0x080485b6 : push cs ; xor byte ptr [edx], al ; dec eax ; push cs ; adc al, 0x41 ; ret
0x08048455 : push ebx ; call 0x8048357
0x0804836c : push es ; ja 0x8048373 ; ret
0x08048454 : push esi ; push ebx ; call 0x8048358
0x080483a3 : rcl cl, 1 ; clc ; jne 0x80483ae ; ret
0x080482ba : ret
0x0804839e : ret 0xeac1
0x0804842a : ret 0xfffe
0x08048387 : ror cl, 1 ; ret
0x080483c4 : ror cl, cl ; ret
0x080483a4 : sar eax, 1 ; jne 0x80483ad ; ret
0x08048351 : sbb al, 0x24 ; ret
0x080484ab : sbb al, 0x5b ; pop esi ; pop edi ; pop ebp ; ret
0x0804839f : shr edx, 0x1f ; add eax, edx ; sar eax, 1 ; jne 0x80483b2 ; ret
0x08048422 : sub byte ptr [ebp + 0x489e845], cl ; and al, 0xe8 ; ret 0xfffe
0x080482b1 : sub esp, 8 ; call 0x8048359
0x080482ca : xor al, byte ptr [eax] ; add byte ptr [eax], al ; add esp, 8 ; pop ebx ; ret
0x080485b7 : xor byte ptr [edx], al ; dec eax ; push cs ; adc al, 0x41 ; ret
0x080484cf : xor ebx, dword ptr [ebx] ; add byte ptr [eax], al ; add esp, 8 ; pop ebx ; ret
