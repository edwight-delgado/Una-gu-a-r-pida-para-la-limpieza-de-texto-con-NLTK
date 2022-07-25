# Una guía rápida para la limpieza de texto usando la biblioteca nltk

## Eliminando espacios extra
<p>La mayoría de las veces, los datos de texto que tiene pueden contener espacios adicionales entre las palabras, después o antes de una oración. Entonces, para comenzar, eliminaremos estos espacios adicionales de cada oración usando expresiones regulares.</p>




```python
import re
doc = "NLP  is an interesting    field.  "
new_doc = re.sub("\s+"," ", doc)
print(new_doc)
```

    NLP is an interesting field. 


## Eliminación de puntuaciones.
<p>Las puntuaciones presentes en el texto no agregan valor a los datos. La puntuación, cuando se adjunta a cualquier palabra, creará un problema al diferenciar con otras palabras.</p>


```python
text = "Hello! How are you!! I'm very excited that you're going for a trip to Europe!! Yayy!"
re.sub("[^-9A-Za-z ]", "" , text)
```




    'Hello How are you Im very excited that youre going for a trip to Europe Yayy'



## Normalización de casos
<p>En esto, simplemente convertimos el caso de todos los caracteres en el texto a mayúsculas o minúsculas. Como python es un lenguaje que distingue entre mayúsculas y minúsculas, tratará a NLP y NLP de manera diferente. Uno puede convertir fácilmente la cadena a inferior o superior usando:
<strong> str.inferior() o str.superior() </strong>.</p>

<p>Por ejemplo, puede convertir el carácter a minúsculas o mayúsculas al momento de verificar los signos de puntuación.</p>


```python
import string
text = "Hello! How are you!! I'm very excited that you're going for a trip to Europe!! Yayy!"
text_clean = "".join([i.lower() for i in text if i not in string.punctuation])
text_clean
```




    'hello how are you im very excited that youre going for a trip to europe yayy'



## Tokenization 
<p>Dividir una oración en palabras y crear una lista, es decir, cada oración es una lista de palabras. Existen principalmente 3 tipos de tokenizadores.</p>

<p>a. word_tokenize: Es un tokenizador genérico que separa palabras y puntuaciones. Un apóstrofo no se considera como puntuación aquí.</p>


```python
import nltk 
text = "Hello! How are you!! I'm very excited that you're going for a trip to Europe!! Yayy!"
nltk.tokenize.word_tokenize(text)
```




    ['Hello',
     '!',
     'How',
     'are',
     'you',
     '!',
     '!',
     'I',
     "'m",
     'very',
     'excited',
     'that',
     'you',
     "'re",
     'going',
     'for',
     'a',
     'trip',
     'to',
     'Europe',
     '!',
     '!',
     'Yayy',
     '!']



## regexp_tokenize
<p>Se puede utilizar cuando queremos separar palabras de nuestro interés que siguen un patrón común
como extraer todos los hashtags de tweets, direcciones de tweets o hipervínculos del texto.</p>
<p>En esto, puede usar las funciones normales de expresiones regulares para separar las palabras.</p>



```python
import re
a = 'What are your views related to US elections @nitin'
re.split('\s@', a)
```




    ['What are your views related to US elections', 'nitin']



## Removing Stopwords
<p>Las palabras vacías incluyen: I, he, she y, but, was were, being, have, etc., que no agregan significado a los datos.
Por lo tanto, estas palabras deben eliminarse, lo que ayuda a reducir las características de nuestros datos. Estos se eliminan después de tokenizar el texto.</p>



```python
stopwords = nltk.corpus.stopwords.words('english')
text = "Hello! How are you!! I'm very excited that you're going for a trip to Europe!! Yayy!"
text_new = "".join([i for i in text if i not in string.punctuation])
print(text_new)
words = nltk.tokenize.word_tokenize(text_new)
print(words)
words_new = [i for i in words if i not in stopwords]
print(words_new)

```

    Hello How are you Im very excited that youre going for a trip to Europe Yayy
    ['Hello', 'How', 'are', 'you', 'Im', 'very', 'excited', 'that', 'youre', 'going', 'for', 'a', 'trip', 'to', 'Europe', 'Yayy']
    ['Hello', 'How', 'Im', 'excited', 'youre', 'going', 'trip', 'Europe', 'Yayy']


## Lemmatization & Stemming

<p> una. Stemming: Una técnica que lleva la palabra a su forma raíz. Simplemente elimina los sufijos de las palabras.
La palabra derivada puede no ser parte del diccionario, es decir, no necesariamente dará significado.
Hay dos tipos principales de Stemmer: Porter Stemmer y Snow Ball Stemmer (versión avanzada de Porter Stemmer).</p>


```python
ps = nltk.PorterStemmer()
w = [ps.stem(word) for word in words_new]
print(w)
```

    ['hello', 'how', 'im', 'excit', 'your', 'go', 'trip', 'europ', 'yayi']



```python
ss = nltk.SnowballStemmer(language = 'english')
w = [ss.stem(word) for word in words_new]
print(w)
```

    ['hello', 'how', 'im', 'excit', 'your', 'go', 'trip', 'europ', 'yayi']


## Lemmatization
<p>Lleva la palabra a su forma raíz llamada Lema. Ayuda a llevar las palabras a su forma de diccionario. Se aplica a los sustantivos por defecto.
Es más preciso ya que utiliza un análisis más informado para crear grupos de palabras con significados similares según el contexto.
por lo que es complejo y lleva más tiempo. Esto se usa cuando necesitamos retener la información contextual.</p>




```python
wn = nltk.WordNetLemmatizer()
w = [wn.lemmatize(word) for word in words_new]
print(w)
```

    ['Hello', 'How', 'Im', 'excited', 'youre', 'going', 'trip', 'Europe', 'Yayy']


## Notas finales
<p> Estas son las técnicas de limpieza que se deben aplicar para que nuestros datos de texto estén listos para el análisis y la construcción de modelos. No es necesario que tengas que realizar todos estos pasos para la limpieza.</p>

Fuente: https://www.analyticsvidhya.com/blog/2020/11/text-cleaning-nltk-library/
