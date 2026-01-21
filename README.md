<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Network Status Dashboard - SMK TKJ</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: linear-gradient(135deg, #0c2461, #1e3799);
            color: #fff;
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
        }

        header {
            text-align: center;
            margin-bottom: 30px;
            padding-top: 20px;
        }

        .logo {
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 15px;
            margin-bottom: 10px;
        }

        .logo i {
            font-size: 2.5rem;
            color: #3498db;
        }

        h1 {
            font-size: 2.5rem;
            margin-bottom: 5px;
            color: #fff;
            text-shadow: 0 2px 4px rgba(0, 0, 0, 0.3);
        }

        .subtitle {
            color: #bdc3c7;
            font-size: 1.1rem;
            margin-bottom: 30px;
        }

        .current-time {
            background-color: rgba(255, 255, 255, 0.1);
            display: inline-block;
            padding: 10px 20px;
            border-radius: 50px;
            margin-top: 10px;
            font-weight: 600;
            border: 1px solid rgba(255, 255, 255, 0.2);
        }

        .dashboard {
            display: flex;
            flex-wrap: wrap;
            gap: 25px;
            justify-content: center;
            margin-bottom: 40px;
        }

        .server-card {
            background-color: #2c3e50;
            border-radius: 15px;
            padding: 25px;
            width: 100%;
            max-width: 350px;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
            transition: transform 0.3s, box-shadow 0.3s;
            border: 1px solid rgba(255, 255, 255, 0.1);
        }

        .server-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
        }

        .server-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
            padding-bottom: 15px;
        }

        .server-title {
            font-size: 1.5rem;
            font-weight: 700;
            color: #3498db;
        }

        .icon {
            font-size: 2.5rem;
            color: #3498db;
        }

        .server-info {
            margin-bottom: 20px;
        }

        .info-row {
            display: flex;
            margin-bottom: 12px;
            align-items: center;
        }

        .info-label {
            width: 90px;
            color: #bdc3c7;
            font-weight: 500;
        }

        .info-value {
            color: #ecf0f1;
            font-weight: 600;
        }

        .status-container {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-top: 25px;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .status-label {
            font-weight: 600;
            color: #bdc3c7;
        }

        .status-box {
            padding: 8px 20px;
            border-radius: 50px;
            font-weight: 700;
            text-transform: uppercase;
            font-size: 0.9rem;
            letter-spacing: 1px;
        }

        .online {
            background-color: rgba(46, 204, 113, 0.2);
            color: #2ecc71;
            border: 2px solid #2ecc71;
        }

        .offline {
            background-color: rgba(231, 76, 60, 0.2);
            color: #e74c3c;
            border: 2px solid #e74c3c;
        }

        .maintenance {
            background-color: rgba(241, 196, 15, 0.2);
            color: #f1c40f;
            border: 2px solid #f1c40f;
        }

        .controls {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
        }

        .refresh-btn {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.1rem;
            border-radius: 50px;
            cursor: pointer;
            font-weight: 600;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
            display: inline-flex;
            align-items: center;
            gap: 10px;
        }

        .refresh-btn:hover {
            background: linear-gradient(135deg, #2980b9, #3498db);
            transform: translateY(-3px);
            box-shadow: 0 8px 20px rgba(52, 152, 219, 0.6);
        }

        .refresh-btn:active {
            transform: translateY(0);
        }

        footer {
            text-align: center;
            margin-top: 50px;
            padding: 20px;
            color: #7f8c8d;
            font-size: 0.9rem;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        @media (max-width: 768px) {
            .dashboard {
                flex-direction: column;
                align-items: center;
            }
            
            .server-card {
                max-width: 100%;
            }
            
            h1 {
                font-size: 2rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <div class="logo">
                <i class="fas fa-network-wired"></i>
            </div>
            <h1>NETWORK STATUS DASHBOARD</h1>
            <div class="subtitle">SMK Teknik Komputer dan Jaringan</div>
            <div class="current-time">
                <i class="far fa-clock"></i> 24 Januari 2025, 14:30 WIB
            </div>
        </header>

        <div class="dashboard">
            <!-- SERVER 1 -->
            <div class="server-card">
                <div class="server-header">
                    <div class="server-title">MikroTik Gateway</div>
                    <div class="icon">
                        <i class="fas fa-router"></i>
                    </div>
                </div>
                <div class="server-info">
                    <div class="info-row">
                        <div class="info-label">IP Address:</div>
                        <div class="info-value">192.168.1.1</div>
                    </div>
                    <div class="info-row">
                        <div class="info-label">Uptime:</div>
                        <div class="info-value">24 Hari 15 Jam</div>
                    </div>
                    <div class="info-row">
                        <div class="info-label">Fungsi:</div>
                        <div class="info-value">Gateway Utama Jaringan</div>
                    </div>
                </div>
                <div class="status-container">
                    <div class="status-label">Status Server:</div>
                    <div class="status-box online">Online</div>
                </div>
            </div>

            <!-- SERVER 2 -->
            <div class="server-card">
                <div class="server-header">
                    <div class="server-title">Server CBT Ujian</div>
                    <div class="icon">
                        <i class="fas fa-server"></i>
                    </div>
                </div>
                <div class="server-info">
                    <div class="info-row">
                        <div class="info-label">IP Address:</div>
                        <div class="info-value">192.168.6.20</div>
                    </div>
                    <div class="info-row">
                        <div class="info-label">Uptime:</div>
                        <div class="info-value">5 Jam</div>
                    </div>
                    <div class="info-row">
                        <div class="info-label">Fungsi:</div>
                        <div class="info-value">Ujian CBT Sekolah</div>
                    </div>
                </div>
                <div class="status-container">
                    <div class="status-label">Status Server:</div>
                    <div class="status-box offline">Offline</div>
                </div>
            </div>

            <!-- SERVER 3 -->
            <div class="server-card">
                <div class="server-header">
                    <div class="server-title">NAS File Server</div>
                    <div class="icon">
                        <i class="fas fa-database"></i>
                    </div>
                </div>
                <div class="server-info">
                    <div class="info-row">
                        <div class="info-label">IP Address:</div>
                        <div class="info-value">192.168.50.5</div>
                    </div>
                    <div class="info-row">
                        <div class="info-label">Uptime:</div>
                        <div class="info-value">12 Hari 8 Jam</div>
                    </div>
                    <div class="info-row">
                        <div class="info-label">Fungsi:</div>
                        <div class="info-value">Penyimpanan File Sekolah</div>
                    </div>
                </div>
                <div class="status-container">
                    <div class="status-label">Status Server:</div>
                    <div class="status-box maintenance">Maintenance</div>
                </div>
            </div>
        </div>

        <div class="controls">
            <button class="refresh-btn" id="refreshBtn">
                <i class="fas fa-sync-alt"></i> REFRESH STATUS
            </button>
        </div>

        <footer>
            <p>Laporan Akhir Layanan Jaringan - SMK TKJ</p>
            <p>© 2025 Tim Jaringan Sekolah. Semua hak dilindungi.</p>
        </footer>
    </div>

    <script>
        // Fungsi untuk mengupdate waktu saat ini
        function updateCurrentTime() {
            const now = new Date();
            const options = { 
                weekday: 'long', 
                year: 'numeric', 
                month: 'long', 
                day: 'numeric',
                hour: '2-digit',
                minute: '2-digit',
                hour12: false
            };
            
            const formatter = new Intl.DateTimeFormat('id-ID', options);
            const formattedDate = formatter.format(now);
            
            document.querySelector('.current-time').innerHTML = 
                `<i class="far fa-clock"></i> ${formattedDate} WIB`;
        }
        
        // Update waktu setiap detik
        setInterval(updateCurrentTime, 1000);
        updateCurrentTime();
        
        // Fungsi untuk tombol refresh
        document.getElementById('refreshBtn').addEventListener('click', function() {
            const btn = this;
            const originalText = btn.innerHTML;
            
            // Animasi loading
            btn.innerHTML = '<i class="fas fa-spinner fa-spin"></i> Memperbarui...';
            btn.disabled = true;
            
            // Simulasi proses refresh
            setTimeout(() => {
                // Random status untuk server CBT (untuk demo)
                const server2Status = document.querySelector('.server-card:nth-child(2) .status-box');
                const statuses = ['online', 'offline', 'maintenance'];
                const currentStatus = server2Status.classList[1];
                let newStatus;
                
                // Pilih status yang berbeda dari saat ini
                do {
                    newStatus = statuses[Math.floor(Math.random() * statuses.length)];
                } while (newStatus === currentStatus);
                
                // Update kelas dan teks status
                server2Status.className = 'status-box ' + newStatus;
                server2Status.textContent = newStatus.charAt(0).toUpperCase() + newStatus.slice(1);
                
                // Update uptime server CBT secara acak
                const server2Uptime = document.querySelector('.server-card:nth-child(2) .info-row:nth-child(2) .info-value');
                const hours = Math.floor(Math.random() * 24);
                const minutes = Math.floor(Math.random() * 60);
                server2Uptime.textContent = `${hours} Jam ${minutes} Menit`;
                
                // Kembalikan tombol ke keadaan semula
                btn.innerHTML = originalText;
                btn.disabled = false;
                
                // Tampilkan notifikasi
                alert('Status server telah diperbarui! Server CBT Ujian sekarang: ' + 
                      newStatus.toUpperCase());
            }, 1500);
        });
        
        // Tambahkan efek hover pada kartu server
        const serverCards = document.querySelectorAll('.server-card');
        serverCards.forEach(card => {
            card.addEventListener('mouseenter', function() {
                this.style.transform = 'translateY(-5px)';
                this.style.boxShadow = '0 15px 30px rgba(0, 0, 0, 0.3)';
            });
            
            card.addEventListener('mouseleave', function() {
                this.style.transform = 'translateY(0)';
                this.style.boxShadow = '0 10px 20px rgba(0, 0, 0, 0.2)';
            });
        });
    </script>
</body>
</html>
