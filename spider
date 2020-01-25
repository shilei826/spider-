import requests
import sys
from bs4 import BeautifulSoup


class downloader(object):
    def __init__(self):
        self.server = 'http://www.kanshu8.net'#主网址
        self.target = 'http://www.kanshu8.net/book/23603/'#需要抓取的网址
        self.names = []#名字
        self.urls = []#链接
        self.nums = 0

    # 获取下载地址
    def get_download_url(self):
        req = requests.get(url=self.target)
        html = req.text
        div_bf = BeautifulSoup(html, 'lxml')
        div = div_bf.find_all('div', class_='pt-chapter-cont-detail full')
        a_bf = BeautifulSoup(str(div[0]), 'lxml')
        a = a_bf.find_all('a')
        self.nums = len(a[:])
        for each in a[:]:
            self.names.append(each.string)
            self.urls.append(self.server+each.get('href'))
            if(a[:] == 0):
                continue

    # 获取章节内容
    def get_contents(self, target):
        #target = 'http://www.kanshu8.net/book/23603/read_21725008.html'
        req = requests.get(url=target)
        html = req.text
        bf = BeautifulSoup(html, 'lxml')
        texts = bf.find_all('div', class_='size16 color5 pt-read-text')
        # print(texts[0].text.replace('\xa0'*8,'\n\n'))
        texts = texts[0].text.replace('\xa0'*8, '\n\n')
        return texts

    # 将抓取的文章内容写入文件
    def writer(self, name, path, text):
        write_flag = True
        with open(path, 'a', encoding='utf-8') as f:
            f.write(name+'\n')
            f.writelines(text)
            f.write('\n\n')


# 主函数
if __name__ == "__main__":
    dl = downloader()
    dl.get_download_url()
    print('<上门女婿叶辰>开始下载:')
    for i in range(dl.nums):
        dl.writer(dl.names[i], '上门女婿叶辰.txt', dl.get_contents(dl.urls[i]))
        print(dl.names[i],dl.urls[i])
        sys.stdout.write("已下载:%.3f%%" % float(i/dl.nums)+'\r')
        sys.stdout.flush()
    print('<上门女婿叶辰>下载完成')
