<div align="center">
<h1>VPN com Tailscale + OPNsense em ambiente CGNAT</h1>
</div>

<div align="center">
<img src="https://img.shields.io/badge/OPNsense-26.1+-blue"/>
<img src="https://img.shields.io/badge/Tailscale-1.80+-purple"/>
<img src="https://img.shields.io/badge/FreeBSD-14+-red"/>

##
Acesse sua rede local de qualquer lugar, mesmo sem IP fixo e com CGNAT

</div>

O Problema

Provedores de internet no Brasil e em todo o mundo estão adotando massivamente o CGNAT (Carrier-Grade NAT) como solução para a escassez de endereços IPv4. Significando que:

Você não tem um IP público roteável - Seu modem recebe um IP privado (geralmente 10.x.x.x ou 100.64.x.x)

Port forwarding não funciona - As portas que você abre no modem não são acessíveis externamente (por serem divididas com outras pessoas)

VPNs tradicionais são impossíveis - WireGuard, OpenVPN e IPsec dependem de portas abertas ou IP público/fixo

Dynamic DNS se torna inútil - Mesmo com DNS apontando, o tráfego não chega até você

<img width="3420" height="1094" alt="deepseek_mermaid_20260317_e1f32b" src="https://github.com/user-attachments/assets/b7cf0b62-d53f-4845-8881-30fc7d2b3ab7" />

A Solução

O Tailscale resolveu esse problema utilizando:
Arquitetura Mesh VPN

Cada dispositivo se conecta diretamente a outros dispositivos (peer-to-peer), sem necessidade de um servidor central.
NAT Traversal (ICE/STUN)

Autenticação baseada em identidade, não em IPs.
Baseado em WireGuard

<img width="2090" height="2146" alt="deepseek_mermaid_20260317_614eae" src="https://github.com/user-attachments/assets/5172d330-1c63-4246-8492-c8b95c14be45" />

Componentes Implementados

Notebook - IP local (192.168.1.83/24) - IP TUNEL VPN (100.125.16.31)
<img width="1920" height="955" alt="image" src="https://github.com/user-attachments/assets/bcb3d4fc-f7e8-491c-8a50-9fee2314993d" />

Celular - 4G - IP TUNEL VPN (100.126.159.128)
<img width="739" height="1600" alt="image" src="https://github.com/user-attachments/assets/99b68718-137d-46d9-bcce-7d16cd35b1c3" />

VM (OPNsense) - WAN (192.168.1.110/24) - LAN (172.16.56.3/16) - IP TUNEL VPN (100.82.211.29)
Notebook pessoal - 4G - IP VPN (100.126.159.128)
<img width="1910" height="991" alt="image" src="https://github.com/user-attachments/assets/7b790aa7-e544-41a0-aab2-4a1a25883b59" />
