# Glitch Scheme Signature
"""
██████╗░░█████╗░███╗░░░███╗██╗░░██╗███████╗██╗░░░██╗
██╔══██╗██╔══██╗████╗░████║██║░██╔╝██╔════╝╚██╗░██╔╝
██║░░██║██║░░██║██╔████╔██║█████═╝░█████╗░░░╚████╔╝░
██║░░██║██║░░██║██║╚██╔╝██║██╔═██╗░██╔══╝░░░░╚██╔╝░░
██████╔╝╚█████╔╝██║░╚═╝░██║██║░╚██╗███████╗░░░██║░░░
╚═════╝░░╚════╝░╚═╝░░░░░╚═╝╚═╝░░╚═╝╚══════╝░░░╚═╝░░░
                        Made by: Cyb0rgBytes
"""

import socket
import argparse
import threading
import time
import random
import colorama
from colorama import Fore, Style

colorama.init()

def animate_loading():
    chars = "/—\|"  # Animation characters
    for char in chars:
        print("\rScanning " + char, end="", flush=True)
        time.sleep(0.1)

def scan_ports(target, start_port, end_port):
    open_ports = []

    for port in range(start_port, end_port + 1):
        sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        sock.settimeout(0.1)
        result = sock.connect_ex((target, port))
        if result == 0:
            open_ports.append(port)
        sock.close()

    return open_ports

def ping_host(target):
    try:
        socket.gethostbyname(target)
        return True
    except socket.gaierror:
        return False

def scan_wrapper(target, start_port, end_port):
    open_ports = scan_ports(target, start_port, end_port)
    print("\n\nPort Scan Results:")
    if open_ports:
        print(f"{Fore.GREEN}Open Ports: {', '.join(map(str, open_ports))}{Style.RESET_ALL}")
    else:
        print(f"{Fore.RED}No open ports found{Style.RESET_ALL}")

def main():
    parser = argparse.ArgumentParser(description="Simple Port Scanner")
    parser.add_argument("target", help="Target IP address or hostname")
    parser.add_argument("--ping", action="store_true", help="Ping the target")
    parser.add_argument("--start-port", type=int, default=1, help="Start port for scanning (default: 1)")
    parser.add_argument("--end-port", type=int, default=100, help="End port for scanning (default: 100)")
    args = parser.parse_args()

    target = args.target
    start_port = args.start_port
    end_port = args.end_port

    print("Initializing scan...")

    if args.ping:
        if ping_host(target):
            print(f"{Fore.GREEN}Ping successful{Style.RESET_ALL}")
        else:
            print(f"{Fore.RED}Ping failed{Style.RESET_ALL}")

    scan_thread = threading.Thread(target=scan_wrapper, args=(target, start_port, end_port))
    scan_thread.start()

    animate_loading()  # Start animation

    scan_thread.join()

if __name__ == "__main__":
    main()
