import os
import re
import shutil
import zipfile

#把old_words.txt复制到当前文件夹
def copy_file_to_current_folder(file_path):
    shutil.copy(file_path, '.')

file_path = 'mm/old_words.txt'
copy_file_to_current_folder(file_path)
file_path = 'mm/new_words.txt'
copy_file_to_current_folder(file_path)


#替换old_words,.txt文件
def replace_words(file_path, old_word_list_path, new_word_list_path):
    with open(file_path, 'r', encoding='utf-8') as file:
        content = file.read()

    with open(old_word_list_path, 'r', encoding='utf-8') as file:
        old_word_list = [line.strip() for line in file.readlines()]

    with open(new_word_list_path, 'r', encoding='utf-8') as file:
        new_word_list = [line.strip() for line in file.readlines()]

    # 创建一个字典，键是被替换词组，值是替换词组
    word_dict = dict(zip(old_word_list, new_word_list))

    for old_word, new_word in word_dict.items():
        pattern = re.compile(re.escape(old_word), flags=re.DOTALL)
        content = pattern.sub(new_word, content)

    with open(file_path, 'w', encoding='utf-8') as file:
        file.write(content)

#修改old_words.txt
file_path = 'old_words.txt'
old_word_list_path = 'TOC.txt'
new_word_list_path = 'NCX.txt'
replace_words(file_path, old_word_list_path, new_word_list_path)

#修改new_words.txt
file_path = 'new_words.txt'
old_word_list_path = 'TOC.txt'
new_word_list_path = 'NCX.txt'
replace_words(file_path, old_word_list_path, new_word_list_path)

#把要处理的文件复制到当前文件夹
def copy_file(src_folder, src_file, dst_folder='.'):
    src_path = os.path.join(src_folder, src_file)
    dst_path = os.path.join(dst_folder, src_file)
    shutil.copy(src_path, dst_path)

src_folder = 'Converter'
src_file = "book.txt"
copy_file(src_folder, src_file)

#在文件的结尾添加“#注 释”
with open("book.txt", "a") as file:
    file.write("\n#注释</h2>\n")

#把文中注释剪切到新文件cut.txt
def match_sentences(input_file, output_file, patterns):
    with open(input_file, 'r', encoding='utf-8') as f:
        content = f.read()

    sentences = []
    for pattern in patterns:
        sentences.extend(re.findall(pattern, content))

    with open(output_file, 'w', encoding='utf-8') as f:
        for sentence in sentences:
            f.write(sentence + ' ')

# 示例用法
patterns = [r'\n①.+', r'\n②...+',r'\n④..+', r'\n③.+',r'\n⑤.+',]

input_file = 'book.txt'
output_file = 'cut.txt'
match_sentences(input_file, output_file, patterns)

#删除原文件中文中注释
def remove_sentences(file_path, patterns_1):
    with open(file_path, 'r', encoding='utf-8') as file:
        content = file.read()

    for pattern in patterns:
        content = re.sub(pattern, '', content)

    with open(file_path, 'w', encoding='utf-8') as file:
        file.write(content)

patterns_1 = [r'\n①.+\n', r'\n②...+\n',r'\n④..+\n', r'\n③.+\n',r'	⑤.+\n',r'	0..',r'  1..',r'	2..',r'	3..',r'	4..',]
file_path = "book.txt"
remove_sentences(file_path, patterns)

#把注释添加到文末
def add_file_to_end(source_file, target_file):
    # 打开源文件和目标文件
    with open(source_file, 'r') as f1, open(target_file, 'a') as f2:
        # 读取源文件内容
        content = f1.read()
        # 将内容添加到目标文件
        f2.write(content)

source_file = 'cut.txt'
target_file = 'book.txt'
add_file_to_end(source_file, target_file)


#剪切版权页和目录页
def copy_n_lines(src_file, dest_file, n):
    with open(src_file, 'r', encoding='utf-8') as src:
        lines = src.readlines()
    with open(dest_file, 'w', encoding='utf-8') as dest:
        dest.writelines(lines[:n])

src_file = 'book.txt'
dest_file = 'cut.txt'
n = 50
copy_n_lines(src_file, dest_file, n)

#整理txt文档，突出章节名,章节名前加\#
def replace_words(file_path, word_dict):
    with open(file_path, 'r', encoding='utf-8') as file:
        content = file.read()

    for old_word, new_word in word_dict.items():
        pattern = re.compile(re.escape(old_word), flags=re.DOTALL)
        content = pattern.sub(new_word, content)

    with open(file_path, 'w', encoding='utf-8') as file:
        file.write(content)

file_path = 'book.txt'
word_dict =  {   
    "* * *": " ",
    "\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
    "\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n": "\n\n\n",
#    "。\n\n\n":  "。\n\n#",
#    "？\n\n\n":  "？\n\n#",
#    "！\n\n\n": "！\n\n#",
#    "”\n\n\n": "”\n\n#",
#    "）\n\n\n": "）\n\n#",
#    "……\n\n\n":  "……\n\n#",
    "\n\n\n": "\n",
    "\n\n\n\n": "\n",
    "\n\n": "\n",
    "\n\n\n\n": "\n",
    "\n\n\n": "\n",
    "\n\n\n\n\n": "\n",
    "\n\n\n\n\n\n": "\n",
    "\n \n \n": "\n",
    "。\n": "。</p>\n<p>",
    "？\n": "？</p>\n<p>",
    "！\n": "！</p>\n<p>",
    "”\n": "”</p>\n<p>",
    "）\n": "）</p>\n<p>",
    "……\n": "……</p>\n<p>",
    "\n": "",
    "\n": "",
    "\n": "",
    "\n": "",
     "</p><p>": "\n",
     "\n": "</p>\n<p>",
     "</p></p>": "</p>",
     "<p><p>": "<p>",
    # 可以添加任意数量的键值对
}
replace_words(file_path, word_dict)

#处理cut.txt
file_path = 'cut.txt'
word_dict =  {   
    "\n\n\n\n": "\n",
    "\n\n\n\n\n": "\n",
    "\n\n\n\n\n\n": "\n",
    "\n\n\n\n\n\n\n": "\n",
    "\n\n\n\n\n\n\n\n": "\n",
    "\n": "</p>\n<p>",
    "图 书": "<p>#图书</h2>",
    "<p>目录</p>": "#目录</h2>",
    # 可以添加任意数量的键值对
}
replace_words(file_path, word_dict)

#把剪切的开头部分恢复
def copy_lines(src_file, dest_file):
    with open(src_file, 'r', encoding='utf-8') as src:
        lines = src.readlines()
    with open(dest_file, 'r+', encoding='utf-8') as dest:
        dest.writelines(lines)

src_file = 'cut.txt'
dest_file = 'book.txt'
copy_lines(src_file, dest_file)

#先把<p>章节名</p>转换为#章节名</h2>
def replace_words(file_path, old_word_list_path, new_word_list_path):
    with open(file_path, 'r', encoding='utf-8', errors='ignore') as file:
        content = file.read()

    with open(old_word_list_path, 'r', encoding='utf-8') as file:
        old_word_list = [line.strip() for line in file.readlines()]

    with open(new_word_list_path, 'r', encoding='utf-8') as file:
        new_word_list = [line.strip() for line in file.readlines()]

    # 创建一个字典，键是被替换词组，值是替换词组
    word_dict = dict(zip(old_word_list, new_word_list))

    for old_word, new_word in word_dict.items():
        pattern = re.compile(re.escape(old_word), flags=re.DOTALL)
        content = pattern.sub(new_word, content)

    with open(file_path, 'w', encoding='utf-8') as file:
        file.write(content)

file_path = "book.txt"
old_word_list_path = 'old_words.txt'
new_word_list_path = 'new_words.txt'

replace_words(file_path, old_word_list_path, new_word_list_path)


#删除指定文件夹
def delete_html_and_toc(folder_path):
    for file in os.listdir(folder_path):
        if file.endswith(".html") or file == "toc.ncx":
            file_path = os.path.join(folder_path, file)
            os.remove(file_path)
            print(f"已删除文件：{file}")
folder_path = "book"
delete_html_and_toc(folder_path)

#删除旧的txt_part文件夹
folder_path = "txt_part"
shutil.rmtree(folder_path)


#拆分txt转换为html文件
def split_txt_to_files(input_file, output_folder):
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    with open(input_file, 'r', encoding='utf-8') as f:
        content = f.read()

    parts = content.split('#')
    for i, part in enumerate(parts):
        if part.strip():
            with open(os.path.join(output_folder, f'index_split_000{i}.txt'), 'w', encoding='utf-8') as f:
                f.write(part)

def convert_txt_to_html(input_folder, output_2_folder):
    if not os.path.exists(output_2_folder):
        os.makedirs(output_2_folder)

    for file in os.listdir(input_folder):
        if file.endswith('.txt'):
            input_file = os.path.join(input_folder, file)
            output_file = os.path.join(output_2_folder, f'{file[:-4]}.html')

            with open(input_file, 'r', encoding='utf-8') as f:
                content = f.read()

            html_content = f'<html><head><title>Unknown </title></head><body><h2>{content}</body></html>'
            with open(output_file, 'w', encoding='utf-8') as f:
                f.write(html_content)

input_file = 'book.txt'
output_folder = 'txt_part'
input_folder = output_folder
output_2_folder = 'book'
split_txt_to_files(input_file, output_folder)
convert_txt_to_html(output_folder, output_2_folder)


#把ton.ncx复制到当前文件夹
def copy_file_to_current_folder(file_path):
    shutil.copy(file_path, '.')

file_path = 'mm/toc.ncx'
copy_file_to_current_folder(file_path)

#替换ton.ncx目录
def replace_words(file_path, old_word_list_path, new_word_list_path):
    with open(file_path, 'r', encoding='utf-8') as file:
        content = file.read()

    with open(old_word_list_path, 'r', encoding='utf-8') as file:
        old_word_list = [line.strip() for line in file.readlines()]

    with open(new_word_list_path, 'r', encoding='utf-8') as file:
        new_word_list = [line.strip() for line in file.readlines()]

    # 创建一个字典，键是被替换词组，值是替换词组
    word_dict = dict(zip(old_word_list, new_word_list))

    for old_word, new_word in word_dict.items():
        pattern = re.compile(re.escape(old_word), flags=re.DOTALL)
        content = pattern.sub(new_word, content)

    with open(file_path, 'w', encoding='utf-8') as file:
        file.write(content)

file_path = 'toc.ncx'
old_word_list_path = 'TOC.txt'
new_word_list_path = 'NCX.txt'

replace_words(file_path, old_word_list_path, new_word_list_path)


#把替换好的ton.ncx移动到电子书文件解压目录，替换ton.ncx
dst = 'book'
shutil.move("toc.ncx", dst)


#为图书更换封面
def move_and_rename(src_folder, dst_folder, file_name):
    src_file = os.path.join(src_folder, file_name)
    dst_file = os.path.join(dst_folder, 'cover_image.jpg')
    shutil.copy(src_file, dst_file)
src_folder = 'Converter'
dst_folder = 'book'
file_name = '00000.jpg'
move_and_rename(src_folder, dst_folder, file_name)

#把文件打包为zip格式文件

def zip_folder(folder_path, output_zip):
    with zipfile.ZipFile(output_zip, 'w', zipfile.ZIP_DEFLATED) as zipf:
        for root, dirs, files in os.walk(folder_path):
            for file in files:
                zipf.write(os.path.join(root, file), os.path.relpath(os.path.join(root, file), folder_path))

folder_path = 'book'
output_zip = 'book.zip'
zip_folder(folder_path, output_zip)

#zip文件重命名为epub文件
def rename_file(old_name, new_name):
    try:
        os.rename(old_name, new_name)
        print(f"{old_name} 重命名为 {new_name} 成功")
    except FileNotFoundError:
        print(f"文件 {old_name} 不存在")
    except Exception as e:
        print(f"重命名文件时出错： {e}")

old_name = "book.zip"
new_name = input("请输入电子书名字:  ")+"."+"epub"
rename_file(old_name, new_name)

#删除指定文件夹
def delete_html_and_toc(folder_path):
    for file in os.listdir(folder_path):
        if file.endswith(".html") or file == "toc.ncx":
            file_path = os.path.join(folder_path, file)
            os.remove(file_path)
            print(f"已删除文件：{file}")
folder_path = "book"
delete_html_and_toc(folder_path)

#清空旧的txt_part文件夹
def clear_folder(folder_path):
    for filename in os.listdir(folder_path):
        file_path = os.path.join(folder_path, filename)
        try:
            if os.path.isfile(file_path) or os.path.islink(file_path):
                os.unlink(file_path)
            elif os.path.isdir(file_path):
                shutil.rmtree(file_path)
        except Exception as e:
            print('Failed to delete %s. Reason: %s' % (file_path, e))

folder_path = 'txt_part'
clear_folder(folder_path)


#删除指定多个无用文件

def delete_files(file_list):
    for file in file_list:
        if os.path.exists(file):
            os.remove(file)
            print(f"已删除文件：{file}")
        else:
            print(f"文件不存在：{file}")

file_list = ["old_words.txt", "new_words.txt","book.txt", "cut.txt"]
delete_files(file_list)
