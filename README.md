# hello-world
import requests

from bs4 import BeautifulSoup


def get_movies():
	headers = {
	'User-Agent': 'Mozilla/5.0 (Linux; Android 6.0; Nexus 5 Build/MRA58N) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/69.0.3497.100 Mobile Safari/537.36',
	'host':'movie.douban.com'
	}
	# 定义一个空列表
	movie_list = []
	# 遍历电影页
	for i in range(0,10):
		link = "http://movie.douban.com/top250?start='+str(i*25)'"
		r = requests.get(link,headers=headers,timeout=10)
		print(str(i*25),'抓取的状态码',r.status_code)

		soup = BeautifulSoup(r.text,'lxml')
		div_list = soup.find_all('div',class_ = 'hd')
		for each in div_list:
			movie = each.a.span.text.strip()
			movie_list.append(movie)

	return movie_list

movies = get_movies()
print(movies)
