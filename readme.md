# Черновик

Информация из блокчейнов криптовалют возможно не достаточна, но точно необходима для анализа и прогноза. Поэтому в начале соберём датасет, в качестве признаков возьмем [отсюда](https://www.blockchain.com/explorer/charts)

Реализуем три подхода:

1. LSTM:
   1. Encoder-only.
   2. Снимаем с выхода последней ячейки цену или класс -- пошла ли цена вверх или нет
2. Transformer
   1. Encoder-only.
   2. Переводим выход в цену или класс (среднее по всем токенам -> линейный слой)
3. Pre-trained transformer
   1. Encoder-only.
   2. Предобучаем с "head" восстанавливать цену
   3. Ипспользуем предобученные слои чтобы предсказать цену или класс

> Мотивация не подбирать forecast length, если мы используем дневные данные:
>
> * за день волатильность достаточная, чтобы цена следующего дня отличалась больше чем на размер комиссии
> * в существующих работах особого профита нет и на одном дне, соотв нет смысла делать seq2seq на 14 дней, например, если уже первый день предсказывается недостаточно корректно, то не стоит ожидать хорошего предсказания последующих дней, где это некорректное предсказание будет использовано