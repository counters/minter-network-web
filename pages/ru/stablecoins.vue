<script>
import {getPool, getStatus} from '~/api/explorer.js';
import {prettyRound, pretty, getApy} from '~/assets/utils.js';
import {HOST} from '~/assets/variables.js';
import trackClick from '~/assets/v-track-click.js';
import Language from '~/layouts/_language.vue';
import Footer from '~/layouts/_footer.vue';

export default {
    layout: 'simple',
    components: {
        Language,
        Footer,
    },
    directives: {
        trackClick,
    },
    fetchOnServer: false,
    fetch() {
        const bipPricePromise = getStatus()
            .then((status) => {
                this.bipPrice = status.bipPriceUsd;
            });

        const poolsPromise = Promise.all([
                getPool('USDCE', 'USDTE'),
                getPool('BEE', 'MUSD'),
                getPool('HUB', 'HUBABUBA'),
            ])
            .then((pools) => {
                this.pools = pools;
                this.hubPrice = pools[1].amount1 / pools[1].amount0;
            });

        return Promise.all([
            bipPricePromise,
            poolsPromise,
        ]);
    },
    head() {
        const title = 'Зарабатывайте 36.5% (APR) в пуле USDT-USDC на Minter';
        const description = 'Не уверены, куда пойдет рынок в ближайшее время? Присоединяйтесь к нашей простой, безопасной и быстрой программе по фармингу стейблкоинов.';
        // const localeSuffix = this.$i18n.locale === 'en' ? '' : '-' + this.$i18n.locale;

        return {
            title: title + ' | Minter Network',
            meta: [
                { hid: 'og-title', name: 'og:title', content: title },
                { hid: 'description', name: 'description', content: description },
                { hid: 'og-description', name: 'og:description', content: description },
                { hid: 'og-image', name: 'og:image', content: `/bipx/images/stablecoins-meta.png` },
            ],
            link: [
                { rel: 'canonical', href: `${HOST}/stablecoins`},
                { rel: 'stylesheet', href: '/bipx/style.css?2'},
                { rel: 'stylesheet', href: '/bipx/style320.css?2', media: '(max-width: 760px)'},
            ],
        };
    },
    data() {
        return {
            bipPrice: 0,
            hubPrice: 0,
            pools: [],
        };
    },
    methods: {
        pretty,
        prettyRound,
        usdPrice(bipValue) {
            return bipValue * (this.bipPrice || 0);
        },
        apy(pool) {
            if (!pool) {
                return 0;
            }
            return getApy(pool.tradeVolumeBip1D, pool.liquidityBip);
        },
    },
};
</script>

<template>
    <div class="wrap">
        <div class="u-container u-container--full index-language">
            <language class="" :locales='[{"code":"","name":"English"},{"code":"ru","name":"Russian"}]' lang="ru" :push="true"/>
        </div>
        <header>
            <div class="top_r">
                <div class="logo"><a href="#"><img src="/img/minter-logo-white.svg" width="155" height="48" alt="Minter"/></a></div>
                <h1>Зарабатывайте 36.5% (APR) в пуле USDT-USDC на Minter</h1>
                <div class="top_e">Не уверены, куда пойдет рынок в ближайшее время? Присоединяйтесь к нашей простой, безопасной и быстрой программе по фармингу стейблкоинов.</div>
                <a class="btn" href="https://www.minter.network/ru/howto/usdt-usdc" target="_blank" v-track-click="'stablecoins-learn'">Начать сейчас</a>
            </div>
            <div class="top_l"><img src="/bipx/images/header-stables.png" srcset="/bipx/images/header-stables@2x.png 2x, /bipx/images/header-stables@3x.png 3x" /></div>
        </header>

        <div class="stablecoins">
            <div class="minter_t">Особенности фарминга стейблкоинов:</div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/stablecoins1.svg" /></div>
                <span>0.1% ежедневно</span>
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/stablecoins2.svg" /></div>
                <span>отсутствие KYC</span>
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/stablecoins3.svg" /></div>
                <span>полностью децентрализованные операции, т.к. Minter — это DEX</span>
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/minter4.svg" /></div>
                <span>легкие ввод и вывод активов</span>
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/stablecoins4.svg" /></div>
                <span>околонулевой риск, т.к. стейблкоины всегда остаются стабильными</span>
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/staking1.svg" /></div>
                <span>до 40% APY дополнительно благодаря комиссиям пула</span>
            </div>
        </div>

        <div class="start">
            <a class="btn" href="https://explorer.minter.network/farming" target="_blank" v-track-click="'stablecoins-farm'">Все программы</a>
        </div>
        <div class="minter">
            <div class="minter_t">Что такое Minter?</div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/minter1.svg" /></div>
                <div class="minter_li_t">Быстрые транзакции</div>
                <span>5 секунд</span> с финальными блоками
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/minter2.svg" /></div>
                <div class="minter_li_t">Низкие комиссии</div>
                <span>$0.01</span> за перевод, <span>$0.03</span> + <span>0.2%</span> за обмен, оплата в любых ликвидных монетах или токенах
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/minter3.svg" /></div>
                <div class="minter_li_t">Кросс-чейн переводы</div>
                Кросс-чейн переводы с обменом. <br />Например, BUSD из Binance Smart Chain на USDC в Ethereum
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/minter4.svg" /></div>
                <div class="minter_li_t">Доступ без преград</div>
                Децентрализованные ввод и вывод, которые легко делать
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/minter5.svg" /></div>
                <div class="minter_li_t">Лимитные ордера</div>
                Лимитные ордера, основанные на уникальной реализации в ядре блокчейна Minter
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/minter6.svg" /></div>
                <div class="minter_li_t">Кастомные токены и пулы</div>
                Создание собственных токенов и пулов ликвидности в несколько кликов
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/minter7.svg" alt=""/></div>
                <div class="minter_li_t">Глобальная интеграция</div>
                Преимущества интеграции с блокчейнами Ethereum и Binance Smart Chain, а в будущем — и другими
            </div>
        </div>
        <div class="minter_bot">Торгуйте большинством криптовалют, токенов и цифровых активов в рамках одной сети. <span>Все — децентрализованно.</span></div>
        <div class="minter_sup">
            <div class="minter_l"><img src="/bipx/images/minter-sup.png" srcset="/bipx/images/minter-sup@2x.png 2x, /bipx/images/minter-sup@3x.png 3x" alt=""/></div>
            <div class="minter_r">
                <div class="minter_sup_t">Minter поддерживает трейдинг и переводы между сетями для</div>
                BTC, ETH, 1INCH, USDT, USDС, DAI, PAX, BUSD, BIP, HUB и многих других.
            </div>
        </div>
        <div class="compare">
            <div class="compare_t">Сравните скорость, комиссии, удобство</div>
            <div class="compare_tab">
                <div class="compare_ths">
                    <div class="compare_1_2">DEX</div>
                    <div class="compare_3">Комиссия пула</div>
                    <div class="compare_4">Скорость</div>
                    <div class="compare_5">Стоимость</div>
                    <div class="compare_6">Необходимо транзакций</div>
                    <div class="compare_7">Комиссии в</div>
                </div>
                <div class="compare_tds">
                    <div class="compare_1"><img src="/img/minter-logo-circle.svg" width="24" height="24" /></div>
                    <div class="compare_2">Minter</div>
                    <div class="compare_3">0.2%</div>
                    <div class="compare_4">5 сек.</div>
                    <div class="compare_5">$0.007</div>
                    <div class="compare_6">1 (<a href="https://explorer.minter.network/transactions/Mt2b9425c1cb91640a8e0dd2207fcc8de8480480b692f4c18fd60f344cbe69b117" target="_blank">Tx</a>)</div>
                    <div class="compare_7">Любой монете</div>
                </div>
                <div class="compare_tds">
                    <div class="compare_1"><img src="/bipx/images/logos/pancakeswap.png" srcset="/bipx/images/logos/pancakeswap@2x.png 2x, /bipx/images/logos/pancakeswap@3x.png 3x" /></div>
                    <div class="compare_2">PancakeSwap</div>
                    <div class="compare_3">0.25%</div>
                    <div class="compare_4">6 сек.</div>
                    <div class="compare_5">$0.27</div>
                    <div class="compare_6">2 (<a href="https://bscscan.com/tx/0xc4655f75d9935e65380046f52e02722f9388273330a3d1ce48593cce7de71c08" target="_blank">Tx</a>, <a href="https://bscscan.com/tx/0xc063cab353d6ca021afe23ee6860787d6cbd286f94f7a8c50434f96dcf1e3d2f" target="_blank">Tx</a>)</div>
                    <div class="compare_7">BNB</div>
                </div>
                <div class="compare_tds">
                    <div class="compare_1"><img src="/bipx/images/logos/uniswap.png" srcset="/bipx/images/logos/uniswap@2x.png 2x, /bipx/images/logos/uniswap@3x.png 3x" /></div>
                    <div class="compare_2">Uniswap</div>
                    <div class="compare_3">0.3%</div>
                    <div class="compare_4">16 сек.</div>
                    <div class="compare_5">$11.4</div>
                    <div class="compare_6">2 (<a href="https://etherscan.io/tx/0x0dc22e02dabda0b5dda7cbc4a997025c6d41af034b8e5b0ab1c002c8f1254485" target="_blank">Tx</a>, <a href="https://etherscan.io/tx/0x191302cbaba0c3ddec945f2a1365f9ca5347790b8f73cf3b69aead37fce77792" target="_blank">Tx</a>)</div>
                    <div class="compare_7">ETH</div>
                </div>
                <div class="compare_tds">
                    <div class="compare_1"><img src="/bipx/images/logos/1inch.png" srcset="/bipx/images/logos/1inch@2x.png 2x, /bipx/images/logos/1inch@3x.png 3x" /></div>
                    <div class="compare_2">1INCH</div>
                    <div class="compare_3">0.3%</div>
                    <div class="compare_4">71 сек.</div>
                    <div class="compare_5">$9.6</div>
                    <div class="compare_6">2 (<a href="https://etherscan.io/tx/0x2918f27fffb09b889a4ca1c34133cb85c21124b8b0feaafc54e6f7ff3abd70bc" target="_blank">Tx</a>, <a href="https://etherscan.io/tx/0xbbee60884c8039e8783b3159008787fb99883380ac49b47f4e3015330b8ac2fb" target="_blank">Tx</a>)</div>
                    <div class="compare_7">ETH</div>
                </div>
                <div class="compare_tds">
                    <div class="compare_1"><img src="/bipx/images/logos/sushiswap.png" srcset="/bipx/images/logos/sushiswap@2x.png 2x, /bipx/images/logos/sushiswap@3x.png 3x" /></div>
                    <div class="compare_2">SushiSwap</div>
                    <div class="compare_3">0.3%</div>
                    <div class="compare_4">62 сек.</div>
                    <div class="compare_5">$9.7</div>
                    <div class="compare_6">2 (<a href="https://etherscan.io/tx/0x54d39d6c7388e1dda1813dc847f0b0067adc815b5ae4859a0bbf0061d678e26b" target="_blank">Tx</a>, <a href="https://etherscan.io/tx/0xc596e8b983dcdea03baa1c49965650e1cf1c2927fc786d17917b18c0e52f9ed7" target="_blank">Tx</a>)</div>
                    <div class="compare_7">ETH</div>
                </div>
            </div>
        </div>
        <div class="farmings" v-if="pools.length">
            <div class="farmings_t">Программы фарминга в Minter</div>
            <div class="farming">
                <div class="farming_top">
                    <div class="farming_icos"><img src="/bipx/images/logos/usdt.svg" /><img src="/bipx/images/logos/usdc.svg" /></div>
                    <div class="farming_t">USDT / USDC</div>
                </div>
                <div class="farming_param">
                    <div>Всего в ликвидности (TVL)</div>
                    <div>${{ prettyRound(usdPrice(pools[0].liquidityBip)) }}</div>
                </div>
                <div class="farming_param">
                    <div>Доходность фарминга (APR)</div>
                    <div>36.5%</div>
                </div>
                <div class="farming_param">
                    <div>Доходность стейкинга (APY)</div>
                    <div>{{ pretty(apy(pools[0])) }}%</div>
                </div>
            </div>
            <div class="farming">
                <div class="farming_top">
                    <div class="farming_icos"><img src="https://explorer-static.minter.network/coins/2361.png" /><img src="/bipx/images/logos/musd.svg" /></div>
                    <div class="farming_t">BEE / MUSD</div>
                </div>
                <div class="farming_param">
                    <div>Всего в ликвидности (TVL)</div>
                    <div>${{ prettyRound(usdPrice(pools[1].liquidityBip)) }}</div>
                </div>
                <div class="farming_param">
                    <div>Доходность фарминга (APR)</div>
                    <div>100%</div>
                </div>
                <div class="farming_param">
                    <div>Доходность стейкинга (APY)</div>
                    <div>{{ pretty(apy(pools[1])) }}%</div>
                </div>
            </div>
            <div class="farming">
                <div class="farming_top">
                    <div class="farming_icos"><img src="/bipx/images/logos/hub.svg" /><img src="/bipx/images/logos/hubabuba.svg" /></div>
                    <div class="farming_t">HUB / HUBABUBA</div>
                </div>
                <div class="farming_param">
                    <div>Всего в ликвидности (TVL)</div>
                    <div>${{ prettyRound(usdPrice(pools[2].liquidityBip)) }}</div>
                </div>
                <div class="farming_param">
                    <div>Доходность фарминга (APR)</div>
                    <div>365%</div>
                </div>
                <div class="farming_param">
                    <div>Доходность стейкинга (APY)</div>
                    <div>{{ pretty(apy(pools[2])) }}%</div>
                </div>
            </div>
            <div class="farming farming_all">
                <a href="https://explorer.minter.network/farming" target="_blank">Смотреть все</a>
            </div>
        </div>
        <div class="staking">
            <div class="minter_t">Стейкинг</div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/staking1.svg" /></div>
                <div class="minter_li_t">Делегируйте</div>
                Делегируйте BIP валидаторам сети, чтобы получать BIP в качестве награды (около 40% годовых)
            </div>
            <div class="minter_li">
                <div class="minter_li_i"><img src="/bipx/images/staking2.svg" /></div>
                <div class="minter_li_t">Предоставляйте ликвидность</div>
                Добывайте BTC, ETH, USDT, USDC, 1INCH, BIP, HUB и многие другие, предоставляя ликвидность в пулы. Награда составляет 0.2% от каждого обмена
            </div>
        </div>
        <div class="wallets">
            <div class="wallets_t">Кошельки</div>
            <div class="wallets_i"><img src="/bipx/images/wallets.png" srcset="/bipx/images/wallets@2x.png 2x" alt="" role="presentation" /></div>
            <div class="wallets_r">
                <div class="wallet">
                    <div class="wallet_i"><img src="/bipx/images/logos/bipwallet.svg" /></div>
                    <div class="wallet_t">Bip Wallet</div>
                    <div class="wallet_e">Удобный и многогранный <br />кошелек-приложение для мобильных <br />устройств</div>
                    <div class="wallet_a">
                        <a class="wallet_andr" href="https://minter.link/ios" target="_blank">iOS</a>
                        <a class="wallet_ios" href="https://minter.link/android" target="_blank">Android</a>
                    </div>
                </div>
                <div class="wallet">
                    <div class="wallet_i"><img src="/bipx/images/logos/webwallet.svg" /></div>
                    <div class="wallet_t"><a href="https://wallet.bip.to/" target="_blank">Web Wallet</a></div>
                    <div class="wallet_e">Базовая веб-версия Bip Wallet. Включает весь ключевой функционал по управлению монетами: получение, отправка, делегирование</div>
                </div>
            </div>
            <div class="wallet">
                <div class="wallet_i"><img src="/img/index-wallet-minter.svg" width="48" height="48"/></div>
                <div class="wallet_t"><a href="https://wallet.minter.org/" target="_blank">Minter Wallet</a></div>
                <div class="wallet_e">Самое простое решение для получения и отправки средств. Чтобы начать, достаточно иметь электронную почту</div>
            </div>
            <div class="wallet">
                <div class="wallet_i"><img src="/img/index-wallet-console.svg" width="48" height="48" alt="" role="presentation"/></div>
                <div class="wallet_t"><a href="https://console.minter.network/" target="_blank">Console</a></div>
                <div class="wallet_e">Этот кошелек предлагает наиболее широкий спектр действий: помимо стандартного функционала, вы получаете возможность работать с чеками, выпускать монеты и токены, запускать и настраивать мастерноды, создавать MultiSig-адреса и пулы ликвидности и управлять ими, а также отправлять транзакции, подписанные офлайн</div>
            </div>
        </div>
        <div class="tech">
            <div class="tech_t">Техническая сторона</div>
            <div class="tech_e">В документации вы найдете все, чтобы начать работу с блокчейном Minter, разрабатывать на нем сервисы и приложения или интегрировать его во внутренние процессы вашей организации.</div>
            <div class="tech_a">
                <a class="tech_git" href="https://github.com/MinterTeam" target="_blank">GitHub</a>
                <a class="tech_api" href="https://www.minter.network/docs#node-api" target="_blank">API</a>
                <a class="tech_sdk" href="https://www.minter.network/docs#minter-sdks" target="_blank">SDK</a>
                <a class="tech_doc" href="https://www.minter.network/docs" target="_blank">Docs</a>
                <a class="tech_cons" href="https://console.minter.network/" target="_blank">Console</a>
            </div>
        </div>
        <div class="social">
            <div class="social_t">Соцмедиа</div>
            <div class="social_e">Следите за всеми нашими новостями, объявлениями и новым контентом в социальных сетях и мессенджерах.</div>
            <div class="social_as">
                <div class="social_a social_md"><a href="https://medium.com/@MinterTeam" target="_blank">Medium</a></div>
                <div class="social_a social_tw"><a href="https://twitter.com/MinterTeam" target="_blank">Twitter</a></div>
                <div class="social_a social_rd"><a href="https://www.reddit.com/r/Minter/" target="_blank">Reddit</a></div>
                <div class="social_a social_tc"><a href="tg://resolve?domain=MinterNetwork" target="_blank">Telegram-канал</a></div>
                <div class="social_a social_tg"><a href="tg://join?invite=EafyEVD-HEOxDcv8YyaqNg" target="_blank">Telegram-группа</a></div>
                <div class="social_a social_fb"><a href="https://www.facebook.com/MinterNetwork" target="_blank">Facebook</a></div>
            </div>
        </div>
        <div class="discover">
            <div class="discover_t">Откройте для себя токен HUB</div>
            <div class="discover_top">
                <div class="discover_img"><img src="/bipx/images/discover.svg" /></div>
                <div class="discover_th">Текущая цена <span>${{ pretty(hubPrice) }}</span></div>
                <div class="discover_th">Начальная цена <span>$0.11</span></div>
                <div class="discover_th">Макс. эмиссия <span>1000000</span></div>
                <div class="discover_th">Пулы <span><a href="https://explorer.minter.network/pools/HUB/USDTE" target="_blank">Minter</a> <a href="https://v2.info.uniswap.org/pair/0x3796fee2b555da1356cdcd3e1861263b351a58a0" target="_blank">Ethereum</a></span></div>
                <div class="discover_go"><a class="btn" href="https://minterteam.medium.com/c0a86610f08f" target="_blank" v-track-click="'stablecoins-white-paper'">White paper</a></div>
            </div>
            <!--<div class="discover_chart"><img src="/bipx/images/chart.svg" /></div>-->
            <div class="discover_e">
                <p><a href="https://etherscan.io/token/0x8e9A29e7Ed21DB7c5B2E1cd75e676dA0236dfB45" target="_blank">HUB</a> это нативный токен в блокчейне Minter Hub, который, в свою очередь, является мостом, соединяющим Minter с Ethereum и Binance Smart Chain. HUB — это PoS-токен, и все оракулы получают 1% комиссии от переводов между сетями. HUB также служит резервом для пулов в Minter, Ethereum и Binance Smart Chain.</p>
                <p>Например, Uniswap v3 <a href="https://info.uniswap.org/#/pools/0x27878ae7f961a126755042ee8e5c074ea971511f" target="_blank">HUB-USDT</a>, Uniswap v2 <a href="https://v2.info.uniswap.org/pair/0x3796fee2b555da1356cdcd3e1861263b351a58a0" target="_blank">HUB-USDT</a>, Minter <a href="https://explorer.minter.network/pools/HUB/BIP" target="_blank">HUB-BIP</a>.</p>
            </div>
        </div>
        <div class="start"><a class="btn" href="https://v2.info.uniswap.org/pair/0xb1700c93ddc26ce1d59441c24daef1035444d7b7" target="_blank" v-track-click="'stablecoins-farm'">Перейти к фармингу USDT и BIPx</a></div>
        <Footer class="footer--transparent"/>
    </div>
</template>
