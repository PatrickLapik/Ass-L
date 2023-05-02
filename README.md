	jmp	start
	db	10	; Hardware Timer Interrupt Vector
	db	20	; Keyboard Interrupt Vector

; ===== Hardware Timer =======
	org	10
	nop
	nop
	nop
	nop
	iret
; ============================

; ===== Keyboard Handler =====
	org	20
	CLI		; Prevent re-entrant use
	push	al
	pushf

	in	07
	cmp	al, 0d
	jnz	idle


	popf
	pop	al
	STI
	jmp	step
	iret

; ============================

; ===== Idle Loop ============
start:
	STI		; Set (I) flag
	out	07	; Make keyboard visible
idle:
	
	nop
	nop
	nop
	nop
	jmp	idle
step:
	mov	al,1	out	05
	mov	al,2	out	05
	mov	al,4	out	05
	mov	al,8	out	05
	mov	al,9	out	05
	mov	al,1	out	05
	mov	al,3	out	05
	mov	al,2	out	05
	mov	al,6	out	05
	mov	al,4	out	05
	mov	al,c	out	05
	mov	al,8	out	05
	mov	al,9	out	05
	mov	al,1	out	05
	jmp	step

; ============================
	end
; ============================

