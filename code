import requests
from bs4 import BeautifulSoup
import os
from colorama import Fore, Style
import datetime

# 存放微博数据
weibo = []

# 返回一个 datetime 对象，表示当前的日期和时间 strftime用于格式化日期和时间的方法。它接受一个时间对象作为输入，并将其格式化为指定的字符串格式。
time = datetime.datetime.now()
# 格式化处理 用于内容时间
formatted_time = time.strftime("%Y-%m-%d %H:%M:%S")
# 格式化处理 用于文件时间
formatted_time_1 = time.strftime("%Y-%m-%d %H-%M-%S")


# 获取HTML
def GetHTMLText(url):
    try:
        cookies = {
            # 'SUB': '_2AkMUQgSDf8NxqwJRmPAVzG3laIV-wgnEieKiHvVYJRMxHRl-yT9jqlZetRB6P8IqbNCljWwEXNZNR565QCcw4Oj8Itm5',
            # 'SUBP': '0033WrSXqPxfM72-Ws9jqgMF55529P9D9W5dUnp8K1GLCokNQpQBN_Ma',
            # 'UOR': 'yunpan.cloud,vdisk.weibo.com,yunpan.cloud', 'SINAGLOBAL': '2194849471079.1987.1668924959229',
            # '_s_tentry': '-', 'Apache': '9181367008338.473.1684132886287',
            # 'ULV': '1684132886310:2:1:1:9181367008338.473.1684132886287:1668924959248',
            'SUBP': '0033WrSXqPxfM72 - Ws9jqgMF55529P9D',
            'ULV': '1684158004692:3:2:2:881667697027.8748.1684158004690:1684132886310',
            'SINAGLOBAL': '2194849471079.1987.1668924959229',
            'Apache': '881667697027.8748.1684158004690',
            'SUB': '_2AkMUQgSDf8NxqwJRmPAVzG3laIV-wgnEieKiHvVYJRMxHRl-yT9jqlZetRB6P8IqbNCljWwEXNZNR565QCcw4Oj8Itm5',
            'UOR': 'yunpan.cloud,vdisk.weibo.com,yunpan.cloud',
        }
        r = requests.get(url, timeout=30, cookies=cookies)
        r.raise_for_status()  # 检查响应对象的状态码
        r.encoding = 'utf-8'
        return r.text
    except:
        return ""


# 处理文本
def fillData(soup):
    tr = soup.find_all('tr', class_="")
    n = 1
    for data in tr:
        # 查找当前 tr 标签下的a、span标签
        a = data.find('a')
        span = data.find('span')
        # 处理置顶内容
        i_1 = data.find('i', class_="icon-top")
        if i_1 is not None:
            # print("TOP %s" % a.string)
            # print("\033[32mTop %s \033[0m" % a.string)
            print(Fore.GREEN + "TOP %s" % a.string)
            # 保存置顶数据至列表weibo
            temp = ["TOP ", a.string]
            weibo.append(temp)
            continue
        # 广告处理
        ad = data.find('td', class_="td-01 ranktop")
        if ad is not None and ad.string == '•':
            continue
        if span is not None:
            # print("%2d、%s %s" % (n, a.string, span.string))
            # print("\033[33m%2d\\033[0m\033[36m%s\033[0m \033[37m%s\033[0m" % (n, a.string, span.string))
            print(Fore.YELLOW + "%02d、" % n, end='')
            print(Fore.CYAN + "%s " % a.string, end='')
            print(Fore.RESET + "%s" % span.string)
            # 保存榜单数据至列表weibo
            temp = ["%02d" % n, '、', a.string, ' |', span.string]
            weibo.append(temp)
        else:  # 特殊榜单处理
            # print("%d、%s" % (n, a.string))
            # print("\033[33m%2d、\033[0m\033[36m%s\033[0m" % (n, a.string))
            print(Fore.YELLOW + "%2d、" % n, end='')
            print(Fore.CYAN + "%s" % a.string, )
            # 保存数据至列表weibo
            temp = ["%02d" % n, '、', a.string]
            weibo.append(temp)
        n = n + 1


# 发起HTTP请求获取页面内容
def main():
    url = web_choice()
    html = GetHTMLText(url)
    soup = BeautifulSoup(html, "html.parser")
    fillData(soup)


# <li><a href="summary?cate=realtimehot" title="热搜榜"><i class="woo-font woo-font--navSHot nav-icon"></i>热搜榜</a></li>/
# <li><a href="summary?cate=socialevent" title="要闻榜"><i class="woo-font woo-font--navSWb nav-icon"></i>要闻榜</a></li>/
# <li><a href="summary?cate=entrank" title="文娱榜" class="cur"><i class="ent_rank_icon"></i>文娱榜</a></li>/
# <li><a href="summary?cate=sport" title="体育榜"><i class="sport_rank_icon"></i>体育榜</a></li>
# <li><a href="summary?cate=game" title="游戏榜"><i class="game_rank_icon"></i>游戏榜</a></li>
# 处理榜单选择
def web_choice():
    os.system('cls')  # 清屏
    print("1-热搜榜\t\t2-要闻榜\t\t3-文娱榜\n4-体育榜\t\t5-游戏榜")
    choice = input("请输入你的选择：")
    web = {
        '1': {
            'add': 'summary',
            'name': '热搜榜'
        },
        '2': {
            'add': 'summary?cate=socialevent',
            'name': '要闻榜'
        },
        '3': {
            'add': 'summary?cate=entrank',
            'name': '文娱榜'
        },
        '4': {
            'add': 'summary?cate=sport',
            'name': '体育榜'
        },
        '5': {
            'add': 'summary?cate=game',
            'name': '游戏榜'
        },
    }
    html = 'https://s.weibo.com/top/' + web[choice]['add']
    os.system('cls')
    # print("\033[34m\t微博搜索-热搜榜\033"+'\033[34m %s\033' % (web[choice]['name']))
    print(Fore.LIGHTMAGENTA_EX + "\t微博搜索-" + '%s' % (web[choice]['name']))
    # 保存榜单名称至列表weibo
    weibo.append("微博搜索-" + web[choice]['name'])
    # 时间
    print(Style.RESET_ALL, end='')  # 重置所有样式
    print('截止于：', formatted_time)
    weibo.append('截止于：' + formatted_time)
    return html


# 发起HTTP请求获取页面内容
main()

# 生成名字为“目标榜单 截止时间”的文件 内容为榜单热搜
with open(str(weibo[0]) + ' ' + str(formatted_time_1) + '.txt', 'w+', encoding='utf-8') as file:
    for data1 in weibo:
        for data2 in data1:
            file.write(data2)
        file.write('\n')
    # 检测文件状态
    fileName = str(weibo[0]) + ' ' + str(formatted_time_1) + '.txt'
    if os.path.isfile(fileName):
        filePath = os.path.abspath(fileName)
        # print("\033[36m文件已保存，路径为：+%s\033[0m" % file_path) # 青色
        print(Fore.LIGHTYELLOW_EX + "文件已保存，路径为：%s" % filePath)
    else:
        # print("\033[35m文件保存失败，请重新运行！\033[0m")
        print(Fore.MAGENTA + "文件保存失败，请重新运行！")

print(Style.RESET_ALL, end='')  # 重置所有样式
