
#                                                               1.  Система инициализации Systemd













##                                          homework_lesson_08_SYSTEMD








###                                          Полезные команды, ссылки.

*             [andrey@nix64amd lesson_08_SYSTEMD]$ systemctl cat sshd                        
            
                # /usr/lib/systemd/system/sshd.service
                [Unit]
                Description=OpenSSH server daemon
                Documentation=man:sshd(8) man:sshd_config(5)
                After=network.target sshd-keygen.target
                Wants=sshd-keygen.target

                [Service]
                Type=notify
                EnvironmentFile=-/etc/crypto-policies/back-ends/opensshserver.config
                EnvironmentFile=-/etc/sysconfig/sshd
                ExecStart=/usr/sbin/sshd -D $OPTIONS $CRYPTO_POLICY
                ExecReload=/bin/kill -HUP $MAINPID
                KillMode=process
                Restart=on-failure
                RestartSec=42s

                [Install]
                WantedBy=multi-user.target
            
            
