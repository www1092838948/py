import urllib.request
import urllib.parse
import json
while 1:
    a = input('请输入需要翻译的内容：')
    url = "http://fanyi.youdao.com/translate?smartresult=dict&smartresult=rule"
    head = {}
    head['User-Agint'] = 'Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36'
    data = {}
    data['i']= a
    data['from'] = 'AUTO'
    data['to']= 'AUTO'
    data['smartresult'] = 'dict'
    data['client'] =  'fanyideskweb'
    data['salt'] = '1523447985841'
    data['sign'] = 'cce432f2d512193b53392cbb3c0b7b4c'
    data['doctype']  = 'json'
    data['version'] = '2.1'
    data['keyfrom'] = 'fanyi.web'
    data['action']  = 'FY_BY_REALTIME'
    data['typoResult']  = 'false'

    data = urllib.parse.urlencode(data).encode('utf-8')
    req = urllib.request.Request(url,data,head)
    #或者注释掉head  req = urllib.request.Requset(url,data)
    #               req.add_header('User-Agint','Mozilla/5.0 (Windows NT 10.0; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.181 Safari/537.36')
    response = urllib.request.urlopen(req)
    html = response.read().decode('utf-8')

    # print(json.loads(html))
    target = json.loads(html)
    print('翻译结果：%s' % (target['translateResult'][0][0]['tgt']))
