---
order: 5
title: Как зарабатывать на стейблкоинах USDT и USDC в Minter
description: >-
  Пошаговое руководство о стейкинге стейблкоинов USDT и USDC в сети Minter, которое поможет получать доход от программ фарминга и комиссий пула ликвидности.
---

# Как зарабатывать на стейблкоинах USDT и USDC в Minter

## Как начать

Весь процесс занимает не более 5 минут и состоит всего из 2 основных шагов:

1. Перевести USDT и USDC из Ethereum в Minter
2. Добавить токены в пул ликвидности

После этого остается только получать ежедневные вознаграждения. 

Добавляя ликвидность в пул, стоит помнить несколько правил:

- Токены добавляются в равных пропорциях (например, 100 USDT и 100 USDC), нельзя добавить только один из них
- Добавить и забрать ликвидность можно в любое время

### Шаг 1. Перевод токенов из Ethereum в Minter

Прежде всего нужно перевести токены USDT и USDC из сети Ethereum в сеть Minter. Для этого совершим кросс-чейн перевод, при котором ваши токены будут удержаны в одной сети (Ethereum) и начислены в другой (Minter). Обратный вывод из Minter в Ethereum можно сделать с той же легкостью, что и ввод. Не переживайте за ваши средства, процесс удобного кросс-чейн перевода осуществляется независимым блокчейном Minter Hub, подробнее о нем можно узнать здесь: https://www.minter.network/ru/hub.

Итак, стейблкоины в сети Minter имеют следующие тикеры:

- [USDTE](https://chainik.io/token/USDTE) (Tether USD) — зеркалированный токен [USDT](https://etherscan.io/token/0xdac17f958d2ee523a2206206994597c13d831ec7) из Ethereum
- [USDCE](https://chainik.io/token/USDCE) (USD Coin) — зеркалированный токен [USDC](https://etherscan.io/token/0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48) из Ethereum

Окончание **E** в конце тикера означает, что токен зеркалирован из сети Ethereum.

Зайдем в [Minter Console](https://console.minter.network/ru) (продвинутый кошелек для управления своими токенами и пулами).

Если у вас уже есть seed-фраза от личного адреса в сети Ethereum, она подойдет и здесь, так как у Minter такой же стандарт — просто авторизуйтесь.

![Minter Console](/img/docs/usdt-usdc-1.png)

Либо можете создать новый кошелек, нажав «Сгенерировать seed-фразу». Надежно сохраните фразу, затем авторизуйтесь.

Перейдите в раздел [Deposit & Withdraw](https://console.minter.network/ru/hub). В блоке **Deposit** авторизуйтесь удобным кошельком, например, MetaMask или Trust Wallet.

![Minter Console](/img/docs/usdt-usdc-2.png)

Введите адрес в сети Minter для депозита (по умолчанию вставляется тот, которым вы авторизовались в Minter Console), выберите токен для депозита и его количество: USDTE или USDCE. Оба токена нужно переводить по очереди.

![Minter Console](/img/docs/usdt-usdc-3.png)

Теперь нужно позволить смарт-контракту отправлять с вашего адреса токены, для этого разблокируйте их кнопкой «Unlock» или «Infinite unlock», чтобы при дальнейших переводах выбранного токена не производить эту транзакцию. Подтвердите транзакцию в кошельке.

Остается отправить токены транзакцией Send, для этого нажмите соответствующую кнопку.

![Minter Console](/img/docs/usdt-usdc-4.png)

Перед отправкой убедитесь, что все данные верны, и обратите внимание на комиссии:

- `Total spend`: общая сумма, которая будет списана с кошелька (с учетом всех комиссий)
- `Bridge fee`: комиссия моста, которая составляет 1%
- `Token balance`: баланс токена на вашем адресе
- `Token unlocked`: количество разблокированных токенов на вашем адресе, доступных для отправки в сеть Minter

После того, как вы перевели один из токенов (например, USDT), необходимо перевести второй (например, USDC) в таком же количестве. Для этого выберите второй токен, разблокируйте и отправьте.

### Шаг 2. Добавление в пул ликвидности

После перевода обоих токенов, они отобразятся на балансе.

Теперь можно добавить их в пул, чтобы предоставить свою ликвидность и стать провайдером. В меню Minter Console откройте вкладку [Pools](https://console.minter.network/ru/pool).

Найдите блок **ADD LIQUIDITY TO SWAP POOL** и заполните форму.

![Minter Console](/img/docs/usdt-usdc-5.png)

- `First coin` – выберите USDTE
- `First coin amount` – количество USDTE для добавления в пул
- `Second coin` – выберите USDCE
- `Second coin amount` – количество USDCE для добавления в пул
- `Slippage tolerance` – проскальзывание; процент, на который допускается отклонение количества токенов в момент отправки транзакции
- `Max amount to spend` – ограничение максимального количества токенов в случае проскальзывания

Проверьте правильность заполнения формы и подтвердите транзакцию. Сразу после этого ваша ликвидность в виде USDTE и USDCE добавится в пул.

Теперь вы являетесь провайдером ликвидности пула USDTE-USDCE и будете получать ежедневные вознаграждения по программе фарминга, а также долю от комиссий за обмены внутри пула.

## Размер и частота вознаграждений

Любой участник сети может предоставить свои стейблкоины USDT и USDC в пул ликвидности, получая за это доход, который состоит из:

1. **Фарминга**: от 0.1% ежедневно (или 36.5% годовых). Доход постоянный и ограничен только периодом программы фарминга
2. **Комиссий пула**: 0.2% с каждой сделки. Доход зависит от объемов торгов в пуле

**Фарминг** — это специальная программа дополнительных вознаграждений провайдерам ликвидности, помимо стандартных комиссий за обмены (0.2% с каждого).

До 1 октября 2021 года в Minter действует программа фарминга для пула [USDCE-USDTE](https://chainik.io/pool/USDCE/USDTE):
- Ежедневные выплаты = 0.1% от суммарной ликвидности провайдера (или 36.5% APR)
- Выплата в монете BIP (по курсу на момент выплаты)
