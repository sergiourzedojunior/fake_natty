### README.md

# Título do Projeto: Extremamente Aesthetic ;)

## 📒 Descrição
Este projeto explora o uso de tecnologias de IA para criar imagens que sejam esteticamente mais bonitas. Utilizamos técnicas avançadas de manipulação de imagens em Python para comparar fotos originais com versões melhoradas geradas por IA. O objetivo é aplicar filtros de beleza que suavizam a pele, ajustam brilho e contraste, e removem imperfeições para melhorar a aparência das pessoas nas fotos.

## 🤖 Tecnologias Utilizadas
- Python
- Google Colab
- PIL (Python Imaging Library)
- OpenCV
- Modelos de IA Generativa (ex: OpenAI)

## 🧐 Processo de Criação
1. **Carregamento das Imagens**: As imagens foram carregadas usando a biblioteca PIL.
2. **Aplicação de Filtros de Beleza**: Foram aplicadas várias técnicas para melhorar a estética das imagens, incluindo:
   - **Suavização da Pele**: Utilizamos um desfoque gaussiano combinado com uma técnica de pesos para manter a nitidez.
   - **Aumento de Nitidez**: Melhoramos os detalhes das imagens, especialmente em áreas como olhos e cabelo.
   - **Ajuste de Brilho e Contraste**: Aumentamos a luminosidade e o contraste das imagens para torná-las mais vibrantes.
   - **Ajuste de Cor**: Intensificamos as cores para dar um aspecto mais vivo.
   - **Remoção de Imperfeições**: Utilizamos um filtro de mediana para remover pequenas imperfeições na pele.
3. **Comparação das Imagens**: As imagens originais e as versões manipuladas foram exibidas lado a lado para uma comparação visual.

### Código do Projeto no Google Colab

```python
# Importação das bibliotecas necessárias
from PIL import Image, ImageFilter, ImageEnhance, ImageOps
import matplotlib.pyplot as plt
import cv2
import numpy as np

# Função para carregar e mostrar a imagem
def load_and_show_image(image_path):
    img = Image.open(image_path)
    plt.imshow(img)
    plt.axis('off')
    plt.show()
    return img

# Função para aplicar filtros de beleza
def apply_beauty_filter(image):
    # Convertendo para numpy array
    image_cv = np.array(image)
    
    # Suavização da pele usando técnicas de desfoque gaussiano
    image_cv = cv2.cvtColor(image_cv, cv2.COLOR_RGB2BGR)
    smooth_image = cv2.GaussianBlur(image_cv, (15, 15), 0)
    image_cv = cv2.addWeighted(image_cv, 1.5, smooth_image, -0.5, 0)
    
    # Convertendo de volta para PIL Image
    image_pil = Image.fromarray(cv2.cvtColor(image_cv, cv2.COLOR_BGR2RGB))
    
    # Aumento de nitidez
    enhancer = ImageEnhance.Sharpness(image_pil)
    image_pil = enhancer.enhance(2.0)
    
    # Ajuste de brilho e contraste
    enhancer = ImageEnhance.Brightness(image_pil)
    image_pil = enhancer.enhance(1.2)
    
    enhancer = ImageEnhance.Contrast(image_pil)
    image_pil = enhancer.enhance(1.2)
    
    # Ajuste de cor
    enhancer = ImageEnhance.Color(image_pil)
    image_pil = enhancer.enhance(1.5)
    
    # Remoção de imperfeições
    image_pil = image_pil.filter(ImageFilter.MedianFilter(size=3))
    
    return image_pil

# Caminho das imagens fornecidas
image_paths = [
    '/mnt/data/carminha1.jpg',
    '/mnt/data/furtado1.jpg',
    '/mnt/data/influenciador1.jpg',
    '/mnt/data/lua1.jpg',
    '/mnt/data/madona1.jpg',
    '/mnt/data/negrini1.jpg',
    '/mnt/data/nero1.jpg',
    '/mnt/data/xuxa1.jpg'
]

# Processamento das imagens
for path in image_paths:
    print(f"Processando a imagem: {os.path.basename(path)}")
    img = load_and_show_image(path)
    img_filtered = apply_beauty_filter(img)
    
    # Mostrar imagem filtrada
    plt.imshow(img_filtered)
    plt.axis('off')
    plt.show()
    
    # Salvar a imagem filtrada
    output_path = path.replace(".jpg", "_filtered.jpg")
    img_filtered.save(output_path)
    print(f"Imagem filtrada salva em: {output_path}")
```

## 🚀 Resultados
As imagens processadas apresentam melhorias estéticas perceptíveis, com suavização da pele, ajuste de brilho e contraste, e remoção de imperfeições. As versões manipuladas são comparadas lado a lado com as originais para destacar as mudanças.

## 💭 Reflexão (Opcional)
Criar algo "natty" (natural) com IA apresenta desafios únicos, especialmente ao tentar manter um equilíbrio entre melhorias estéticas e a preservação das características naturais das pessoas. Este projeto destaca a capacidade das ferramentas de IA em melhorar a aparência visual das imagens, ao mesmo tempo em que levanta questões sobre autenticidade e percepção estética.