# 遍历json文件并将字典嵌套的列表转化为数据框
小组project中遇到这样的两个需求，google到了一些零碎的有帮助的帖子，这里记录一下自己的代码。  
我所做的事情大概是这样的：我有一个文件夹，这个文件夹下有很多子文件夹，每个子文件夹下一个json文件，json文件里有两个dictionary，我只需要第一个dictionary的信息，它的key是'users'。最后将所有json文件里关于'users'的信息导出为csv文件。  
参考资料：https://www.codeleading.com/article/12104371606/

## 第一步：遍历文件
先导入一些必要的库。
```python
import os
import json
import pandas as pd
```
遍历文件，返回list类型的变量。
```python
def read_files(path):
    data=[]
    files=os.listdir(path) #得到文件夹下所有文件的名称
    for file in files:
        filepath = path + '/' + file
        print(file)
        if  os.path.isfile(filepath):#如果不是文件夹就打开
            with open(filepath,'r',encoding='UTF-8') as js_file:
                js=json.load(js_file)
                data.append(js)
                print(js)
        elif os.path.isdir(filepath):
            file_data=read_files(filepath)
            data.extend(file_data)
    return data

  content = read_files('D:/project')
  ```
此时content就是存储着所需内容的list变量。
## 第二步：转化数据框  
接下来根据list里所嵌套的内容来定义一个数据框。
```python
df = pd.DataFrame(columns = ['id', 'nickname', 'gender', 'location','birthday','description','verified_reason','talent','education','work','weibo_num','following','followers'])
df
```
然后就可以将content里的内容放进数据框里了。
```python
for data in content:
    data_row = data['user']
    df_newrow = pd.DataFrame({'id':[data_row['id']],
                              'nickname':[data_row['nickname']],
                              'gender':[data_row['gender']],
                              'location':[data_row['location']],
                              'birthday':[data_row['birthday']],
                              'description':[data_row['description']],
                              'verified_reason':[data_row['verified_reason']],
                              'talent':[data_row['talent']],
                              'education':[data_row['education']],
                              'work':[data_row['work']],
                              'weibo_num':[data_row['weibo_num']],
                              'following':[data_row['following']],
                              'followers':[data_row['followers']],
                             })
    df = df.append(df_newrow, ignore_index=True)
```
## 第三步：导出为csv文件
```python
df.to_csv(r'D:\project\repost_userinfo\data.csv',index=False,encoding="utf_8_sig") 
#中文字符需要加上encoding="utf_8_sig"，英文不需要
```
