#Persistent
#NoEnv
SendMode Input
CoordMode, Pixel, Screen
SetBatchLines, -1

; Configurações
aim_color := 0xFF0000 ; Cor do inimigo (vermelho)
tolerance := 5        ; Tolerância na busca da cor
move_speed := 10      ; Velocidade do movimento
active := true        ; Ativo automaticamente

; Loop infinito para busca
SetTimer, AimbotLoop, 1
return

AimbotLoop:
if (active)
{
    PixelSearch, FoundX, FoundY, 0, 0, A_ScreenWidth, A_ScreenHeight, aim_color, tolerance, Fast RGB
    if (ErrorLevel = 0)
    {
        CenterX := A_ScreenWidth / 2
        CenterY := A_ScreenHeight / 2
        DeltaX := (FoundX - CenterX) / move_speed
        DeltaY := (FoundY - CenterY) / move_speed
        MouseMove, DeltaX, DeltaY, 0, R
    }
}
return

; Tecla Q para ligar/desligar
F8::
active := !active
SoundBeep, 750, 300
return
