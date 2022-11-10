import time
import concurrent.futures
from netmiko import ConnectHandler
import datetime


hosts_info = []

starting_time = time.perf_counter()


with open('zte_router_IP.txt', 'r') as devices:
    for line in devices:
        deviceip = line.strip()
        host = {
            'device_type': 'zte_zxros',
            'ip': deviceip,
            'username': 'who',
            'password': 'who',
            'secret': 'zxr10',
            "session_log": 'netmiko_session.log',

        }
        hosts_info.append(host)


connection = ConnectHandler(**host)

def open_connection(host):
    try:
        connection = ConnectHandler(**host)
        print('Connection Established to Host:', host['ip'])
        now = datetime.datetime.now()
        time = (now.strftime("%Y%m%d_%H%M%S"))
        hostname = connection.send_command('show hostname')
        connection.enable()
        connection.config_mode()
        command1 = connection.send_command('show privilege')
        with open(str(hostname)+'_'+str(time)+'.txt', 'w') as f:
            print(command1, file=f)    
        return sendcommand + ' ' + 'For Device:' + host['ip']
    except:
        print('Connection Failed to host', host['ip'])


if __name__ == '__main__':
    with concurrent.futures.ProcessPoolExecutor() as executor:
        results = executor.map(open_connection, hosts_info)
        for result in results:
            print(result)

    finish = time.perf_counter()
    print('Time Elapsed:', finish - starting_time)
