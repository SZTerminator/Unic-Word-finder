def clear_from_simbols(data):
    import re
    data = data.replace("-","_")  # Спасаем дефисы для некоторых слов как "как-нибудь" или "fourty-five"
    regex = re.compile('\W')     # Хз зачем но без этого не работает
    data = regex.sub(' ',data)   # Собственно удаление спец. символов
    data = data.replace("_","-") # Возвращаем дефисы на своё место
    return data

def return_unic(data):
    
    data = set(data)
    data = list(data)
    
    return data
    
def delete_numbers(data):
    
    words = []
    for i in data:
        if i.isdigit():
            continue
        words.append( i )
        
    return words

def read_from_file(name):
    '''Функция принимает имя файла,
    который будет про0чтён и из которого составит и
    вернёт список уникальных слов
    
    name - задаёться полным именем и его директории:
    
    data.txt
    texsts\data.txt
    C:\texsts\data.txt
    
    '''
    
    with open(name,"r") as g:   # Открываем
        data = g.read()                # Читаем и запоминаем
        return data
        
def return_unic_words(name):
    
    data = read_from_file(name)
    data = data.replace('_',' ')     # Убираем исключение _
    data = data.lower()              # Переводим в нижний регистр так как "Мы" и "мы" - одно и тоже слоово
    data = clear_from_simbols(data)
    data = data.split()                          # Делаем из строки список
    data = return_unic(data)
    data = sorted(data)
    data = delete_numbers(data)
    return data

def save_to_file(name,list_of_words):
    with open(name,'w') as f:
        words = len(list_of_words)
        f.write('Количество уникальных слов ' + str(words) + '\n')
        f.write("========================================" + '\n')
        for i in list_of_words:
            f.write(i + '\n')
          
from library import save_to_file
from library import return_unic_words
# from library import read_from_file

data = return_unic_words('data.txt')

save_to_file('count.txt', data)
