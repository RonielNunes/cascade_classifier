O Cascade Classifier é um algoritmo de detecção de objetos implementado na biblioteca OpenCV. Ele é usado para detectar objetos específicos em imagens ou fluxos de vídeo, com base em padrões visuais previamente treinados.

O Cascade Classifier utiliza uma técnica chamada Classificador de Características em Cascata, que é uma abordagem eficiente para detecção de objetos em tempo real. Esse método é baseado no uso de um grande número de características simples (ou fracos classificadores) organizados em cascata.

O treinamento de um Cascade Classifier envolve várias etapas:

1. **Preparação do conjunto de treinamento:** É necessário coletar um grande conjunto de imagens positivas que contenham o objeto de interesse e um conjunto de imagens negativas que não contenham o objeto. Essas imagens são usadas para extrair as características necessárias para o treinamento do classificador.

2. **Extração de características:** As imagens positivas e negativas são processadas para extrair características relevantes, que podem ser formas, texturas ou outros atributos visuais distintivos do objeto que se deseja detectar.

3. **Treinamento inicial:** O treinamento começa com um classificador simples, que é treinado para distinguir entre as características positivas e negativas. Isso envolve o ajuste de pesos e parâmetros para otimizar a detecção e minimizar os falsos positivos e negativos.

4. **Treinamento em cascata:** Nesta etapa, o classificador inicial é refinado em várias iterações. Cada iteração consiste em testar o classificador atualizado em um conjunto de imagens positivas e negativas. Durante o processo, as características irrelevantes são eliminadas, e os classificadores subsequentes são treinados com mais detalhes e precisão.

5. **Ajuste de limiares:** Após o treinamento, são realizados ajustes nos limiares de detecção para equilibrar a sensibilidade e a especificidade do classificador. Isso permite definir o quão rígida ou permissiva será a detecção do objeto.

Uma vez que o Cascade Classifier é treinado, ele pode ser usado para detectar objetos em novas imagens ou fluxos de vídeo. A detecção ocorre percorrendo a imagem em várias escalas e posições, aplicando os classificadores em cascata e verificando se os padrões visuais correspondentes são encontrados. Quando um objeto é detectado, um retângulo delimitador é desenhado ao redor dele.

O Cascade Classifier é amplamente utilizado em várias aplicações, como detecção de rostos, detecção de veículos, reconhecimento de objetos, entre outros, devido à sua eficiência e precisão.

```Python
import cv2

# Carregar o classificador pré-treinado para detecção de rostos
face_cascade = cv2.CascadeClassifier('haarcascade_frontalface_default.xml')

# Carregar a imagem
image = cv2.imread('image.jpg')

# Converter a imagem para escala de cinza
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

# Realizar a detecção de rostos na imagem
faces = face_cascade.detectMultiScale(gray, scaleFactor=1.1, minNeighbors=5, minSize=(30, 30))

# Desenhar retângulos ao redor dos rostos detectados
for (x, y, w, h) in faces:
    cv2.rectangle(image, (x, y), (x+w, y+h), (0, 255, 0), 2)

# Exibir a imagem com os rostos detectados
cv2.imshow('Faces Detectadas', image)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
> Neste exemplo, o código carrega o classificador Haar Cascade pré-treinado para detecção de rostos (arquivo haarcascade_frontalface_default.xml). Em seguida, a imagem é carregada e convertida para escala de cinza. A detecção de rostos é realizada utilizando o método detectMultiScale do Cascade Classifier, que retorna as coordenadas dos retângulos delimitadores dos rostos detectados. Esses retângulos são então desenhados na imagem original.

> Finalmente, a imagem com os rostos detectados é exibida em uma janela. Pressionar qualquer tecla fecha a janela.

> Lembre-se de substituir 'image.jpg' pelo caminho e nome do arquivo de imagem que você deseja usar para detecção de rostos.

# Detecção de Objetos com OpenCV - Tutorial

Este repositório contém um tutorial sobre como realizar detecção de objetos utilizando a biblioteca OpenCV. Neste tutorial, você aprenderá como criar um conjunto de imagens positivas e negativas, realizar a marcação dos objetos de interesse e treinar um classificador Haar Cascade.

## Pré-requisitos

Antes de começar, certifique-se de ter as seguintes dependências instaladas:

- Python (versão X.X.X)
- OpenCV (versão X.X.X)
- Numpy (versão X.X.X)

## Passo 1: Preparação das Imagens

1. Crie as imagens positivas que contêm os objetos a serem detectados e marque-os com uma checkbox.
2. Crie as imagens negativas em preto e branco sem o objeto a ser detectado.

Certifique-se de que as imagens positivas estejam na pasta `positive/raw` e as imagens negativas na pasta `negative`.

## Passo 2: Preenchendo o arquivo `bg.txt`

1. Execute o arquivo `create_list.bat` para preencher o arquivo `bg.txt` com o nome das imagens negativas.

## Passo 3: Recortando as Imagens Positivas

1. Na pasta `positive`, execute o arquivo `objectmarker.exe`.
2. Selecione a parte da imagem que deseja reconhecer. Pressione a tecla de espaço para salvar a detecção.
3. Repita o processo de seleção para cada objeto nas imagens. Pressione Enter para pular as imagens sem objetos.

## Passo 4: Criação dos Amostras

1. Volte para a pasta principal e execute o arquivo `01_samples_creation.bat`. Isso criará arquivos na pasta `vector`.

## Passo 5: Treinamento do Classificador

1. Certifique-se de que a pasta `cascades` esteja limpa.
2. Abra o arquivo `02_harrtraining.bat` em um editor de texto.
3. Altere os parâmetros `-nneg` e `-npos` para o número de imagens negativas e positivas, respectivamente.
4. Salve as alterações e execute o arquivo `02_harrtraining.bat`.

## Passo 6: Conversão do Classificador

1. Após o treinamento, execute o arquivo `03_convert.bat`. Isso gerará o arquivo `.xml` do classificador.

Parabéns! Agora você tem um classificador Haar Cascade treinado para detecção de objetos. Você pode utilizar esse classificador em seus projetos com o OpenCV.

## Recursos Adicionais

Para um tutorial mais detalhado sobre o processo de detecção de objetos com o OpenCV, confira o vídeo tutorial disponível [aqui](https://www.youtube.com/watch?v=FKMd9BnjMqo).
