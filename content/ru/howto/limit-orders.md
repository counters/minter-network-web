---
order: 7
title: >-
  Лимитные ордера в Minter
description: >-
  Руководство по лимитным ордерам: как создавать заявки на покупку или продажу криптовалют в Minter.
---

# Лимитные ордера в Minter

Minter DEX позволяет создавать и исполнять лимитные ордера на покупку или продажу любого актива. Лимитные ордера располагаются внутри пулов ликвидности. Особенностью данного подхода является то, что часть объема пользователя может быть автоматически исполнена через лимитный ордер, а оставшаяся часть через обычный AMM в рамках того же пула. [Подробнее >>](https://daniillashin.medium.com/minter-2-on-chain-automated-market-maker-with-order-book-5c98869682c9)

## Особенности
- За создание и ручную отмену ордеров взимается комиссия: **$0.1** (создание) и **$0.01** (отмена);
- Автоматическая отмена ордеров происходит через 483840 блоков (≈25 дней);
- При автоматической отмене ордеров, комиссия не взимается;
- Создание, отмена и список собственных ордеров доступны во вкладке [Limit Orders](https://console.minter.network/ru/order) в Minter Console;
- Установка цены ордера возможна в диапазонах: x5 (выше) и 1/5 (ниже) от текущей цены пула. *Например, в пуле BIP-USDTE при текущей цене BIP = 0.004 USDTE, максимальная цена продажи для ордера = 0.02 USDTE, минимальная цена покупки = 0.0008 USDTE*;
- Лимитные ордера выставляются "поверх" ликвидности пула, дополняя ее ([подробнее про AMMOB](https://daniillashin.medium.com/minter-2-on-chain-automated-market-maker-with-order-book-5c98869682c9));
- 0.2% от объема исполненного ордера уходит в пул (в обоих токенах, поровну), расширяя его и делая "богаче". Эту комиссию зарабатывают провайдеры ликвидности (при этом не испытывая Impermanent Loss в момент исполнения любых ордеров);
- Допускается частичное исполнение ордера;
- Ордербуки и выставленные ордеров доступны на странице пула в Minter Explore.

## Как создать лимитный ордер
Перейдите во вкладку [Limit Orders](https://console.minter.network/ru/order) в Minter Console. Заполните форму:

![Создание лимитного ордера](/img/docs/limit-1.png)

- Выберите монету, которую продаете, ее количество и цену продажи
- Выберите монету, которую покупаете, ее количество и инвертированная цена посчитаются автоматически

Остается разместить лимитный ордер, подтвердив транзакцию. В данном примере продаются 0.1 BTC по цене 54000 долларов, если ордер исполнится, пользователь получит 5400 USDTE:

![Создание лимитного ордера](/img/docs/limit-2.png)

## Отмена лимитного ордера

Ордера автоматически отменяются через 483840 блоков (≈25 дней), однако, при необходимости их можно отменить и вручную. Для этого нажмите на "–" напротив вашего размещенного ордера в списке ордеров:

![Создание лимитного ордера](/img/docs/limit-3.png)

Идентификатор ордера впишется в поле формы отмены и остается подтвердить транзакцию отзыва:

![Создание лимитного ордера](/img/docs/limit-4.png)

## Руководства
- [Видео-гайд](https://www.youtube.com/watch?v=YdXq0L_kw0c)
- [Обучающий мастер-класс для новичков](https://t.me/MinterNetwork/2432)