awk ѧϰ�ʼ�
==========

�������˼������ܵ���־�������أ������־���������һ���Լ�Ҳ���ֲ������⣬������дһЩ�򵥵ļ�ؽű���������־�Ĵ��������
������û��error��ÿ���ж���error�������� �뵽����ǰ��ά��ͬʱ����awk��������򵥵�ѧϰ�¡�


####����
��򵥵�����ĳЩ�� ʹ��$4 ��������ʾ  __$0__���������

    [root]/root/test$ps -ef|grep uwsgi|awk '{print $1,$5}'
    root Jul24
    root Jul24
    root Jul24
    root Jul24
    root Jul24
    root Jul24
    root Jul24
    root Jul24
    root Jul24
    root 18:49

��ʽ�������

    [root]/root/test$ps -ef|grep uwsgi|awk '{printf "%-2s and %-4s \n",$1,$5}'
    root and Jul24
    root and Jul24
    root and Jul24
    root and Jul24
    root and Jul24
    root and Jul24
    root and Jul24
    root and Jul24
    root and Jul24
    root and 18:51

####���� �ж�
�жϷ��� !=, >, <, >=, <=,==

    [root]/root/test$ps -ef|grep uwsgi|awk '$2=="20596"'
    root     20596 20560  0 Jul24 ?        00:00:19 uwsgi -x uwsgi.xml
    #ʹ�ñ�ͷ(����ȡ��һ��) NR
    [root]/root/test$ps -ef|grep uwsgi|awk '$2=="20596" || NR==1 {print $7}'
    00:00:01
    00:00:19

�ڽ�������
    $0 --->  ��ǰ��¼����������д���������е����ݣ�
    $1~$n --->   ��ǰ��¼�ĵ�n���ֶΣ��ֶμ���FS�ָ�
    FS--->  �����ֶηָ��� Ĭ���ǿո��Tab
    NF--->  ��ǰ��¼�е��ֶθ����������ж�����
    NR--->  �Ѿ������ļ�¼���������кţ���1��ʼ������ж���ļ��������ֵҲ�ǲ����ۼ��С�
    FNR---> ��ǰ��¼������NR��ͬ���ǣ����ֵ���Ǹ����ļ��Լ����к�
    RS--->  ����ļ�¼�ָ����� Ĭ��Ϊ���з�
    OFS---> ����ֶηָ����� Ĭ��Ҳ�ǿո�
    ORS---> ����ļ�¼�ָ�����Ĭ��Ϊ���з�
    FILENAME--->    ��ǰ�����ļ�������

ȡ���ض����в���ʾ�кţ�

    [root]/root/test$ps -ef|grep uwsgi|awk '$2=="20596" || NR==1 {printf "No %s, %s \n",NR,$7}'
    No 1, 00:00:01
    No 6, 00:00:19

ָ���ָ����

    [root]/root/test$awk  'BEGIN{FS=":"} {print $1,$3,$6}' /etc/passwd
    root 0 /root
    bin 1 /bin
    daemon 2 /sbin
    adm 3 /var/adm
    #Ҳ����д��
    awk  -F: '{print $1,$3,$6}' /etc/passwd

����ָ�����д���� awk -F '[;:]'

####ʹ������

    $cat test.log
    2014-07-21 20:00:53,379 - charge - INFO - 30748 - contract_no=chuangfu-MIDS-1306
    2014-07-21 20:00:53,406 - charge - INFO - 30748 - contract_no=chuangfu-MIDS-1306
    2014-07-21 20:00:53,431 - charge - INFO - 30748 - contract_no=chuangfu-MIDS-1306
    2014-07-21 20:00:53,543 - charge - INFO - 30748 - contract_no=vvvgame-CCDL-1307
    2014-07-24 16:00:34,356 - charge - INFO - 18338 - contract_no=sennheiser-CC-1405
    2014-07-24 16:00:34,394 - charge - INFO - 18338 - contract_no=sennheiser-CC-1405
    2014-07-24 16:04:24,431 - charge - INFO - 19081 - contract_no=sennheiser-CC-1405
    2014-07-24 16:04:24,479 - charge - INFO - 19081 - contract_no=sennheiser-CC-1405
    2014-07-24 16:07:20,349 - charge - INFO - 19081 - contract_no=sennheiser-CC-1405
    2014-07-24 16:07:20,390 - charge - INFO - 19081 - contract_no=sennheiser-CC-1405
    [root]/Application/2.0/nirvana/logs$awk '$10 ~ /MIDS/ {print NR,$1,$2}' test.log
    1 2014-07-21 20:00:53,379
    2 2014-07-21 20:00:53,406
    3 2014-07-21 20:00:53,431

���� ~��ģʽ�Ŀ�ʼ������Ƕ�ģʽȡ�� ʹ��!~�� //��������ʽ
�ѽ���ŵ��ļ���ֱ��ʹ���ض�������ˡ�

__ʹ��if else���ļ������ض���__

    $awk '{if($10 ~ /MIDS/) print > "mids.txt";else if($6 ~ /CCDL/) print > "ccdl.txt"; else print > "cc.txt"}' test.log

####Demo  С����

    #����log�ļ��Ĵ�С
    $ls -l *.log|awk '{sum+=$5} END {print sum}'
    102610686
    #��ӡ99�˷���
    $seq 9 | sed 'H;g' | awk -v RS='' '{for(i=1;i<=NF;i++)printf("%dx%d=%d%s", i, NR, i*NR, i==NR?"\n":"\t")}'
    1x1=1
    1x2=2   2x2=4
    1x3=3   2x3=6   3x3=9
    1x4=4   2x4=8   3x4=12  4x4=16
    1x5=5   2x5=10  3x5=15  4x5=20  5x5=25
    1x6=6   2x6=12  3x6=18  4x6=24  5x6=30  6x6=36
    1x7=7   2x7=14  3x7=21  4x7=28  5x7=35  6x7=42  7x7=49
    1x8=8   2x8=16  3x8=24  4x8=32  5x8=40  6x8=48  7x8=56  8x8=64
    1x9=9   2x9=18  3x9=27  4x9=36  5x9=45  6x9=54  7x9=63  8x9=72  9x9=81


####��ôд�ű���������ѧϰ
>����
>[AWK�����̳�](http://coolshell.cn/articles/9070.html)
