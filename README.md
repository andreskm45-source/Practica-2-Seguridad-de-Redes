# Practica-2-Seguridad-de-Redes

graph TD
    %% Definición de estilos
    classDef firewall fill:#f96,stroke:#333,stroke-width:2px;
    classDef server fill:#85c1e9,stroke:#333,stroke-width:2px;
    classDef pc fill:#abebc6,stroke:#333,stroke-width:2px;
    classDef cloud fill:#e5e7e9,stroke:#333,stroke-width:2px,stroke-dasharray: 5 5;

    subgraph Sede A - Usuarios
        U1["💻 PC Usuario (Ubuntu)<br>Red: 10.7.84.0/25<br>IP por DHCP"]:::pc
        F1["🧱 FortiGate 1<br>Gateway LAN: 10.7.84.1"]:::firewall
        U1 -->|VLAN 10| F1
    end

    subgraph Nube Pública
        ISP(("☁️ ISP<br>(Internet)")):::cloud
        F1 -->|WAN (IP Pública)| ISP
        ISP -->|WAN (IP Pública)| F2
        F1 -.->|🔒 Túnel VPN IPsec Site-to-Site 🔒<br>Tráfico Enrutado Exclusivo| F2
    end

    subgraph Sede B - Centro de Datos
        F2["🧱 FortiGate 2<br>Gateway LAN: 10.7.84.129"]:::firewall
        S1["🌐 Web Server (Ubuntu)<br>Red: 10.7.84.128/28<br>IP: 10.7.84.130"]:::server
        F2 -->|Puerto 2| S1
    end
