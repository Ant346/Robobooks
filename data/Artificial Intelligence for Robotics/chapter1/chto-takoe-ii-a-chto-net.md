# Что такое ИИ \(а что нет\)?

Каково определение ИИ? В общем, это машина, обладающая какими-либо характеристиками разумности - мышление, рассуждение, планирование, обучение, адаптация. Также это может быть программа, симулирующая мышление или рассуждение. Приведем пример: робот, избегающий препятствий по простым правила \(если препятствие справа - сворачивай налево\) не является ИИ. Программа, обученная на примерах находить кота на видео - ИИ. Механическая рука, управляемая джойстиком - не ИИ, но рука, адаптирующаяся к объектам, которые она будет поднимать - ИИ.

Существуют две определяющих характеристики ИИ роботов, о которых Вам необходимо знать. Прежде всего, роботы с ИИ обучаются и адаптируются к своему окружению, что означает, что они изменяют своё поведение с течением времени. Вторая характеристика - **эмерджентное поведение**, роботы совершают действия, которые не были программно в них заложены. Мы даём роботу контролирующее ПО которое, по существу, нелинейное и самоорганизующееся. Робот может внезапно проявить неожиданную или удивительную реакцию на странное, необычное событие или ситуацию. Я работал с автомобилем с автоматическим управлением, который \(точно\) обладал тонкими чувствами и двигался очень изысканно, за что получил прозвище _Фердинанд_ в честь чувствительного, любящего цветы быка из мультиков, что очень подходило для девятитонного грузовика, который, похоже, также любил цветы. Такое поведение было вызвано взаимодействием различных программных компонентов и управляющих алгоритмов, и не представляло собой ничего, кроме этого.

Один из концептов, о которых Вы услышите в кругах ИИ - **тест Тьюринга**. Тест Тьюринга был предложен Аланом Тьюрингом в 1950 году, в работе _Computing Machinery and Intelligence_. Он постулировал, что человек-допрашивающий будет одновременно опрашивать систему ИИ и другого человека. Если по итогам разговора он не сможет сказать, кто из допрашиваемых был человеком, а кто ИИ - компьютер успешно пройдет тест. Этот тест предполагает, что ИИ будет способен слушать разговор, понимать его содержание и давать какие-либо ответы на него. Я не думаю, что современный ИИ достиг этой точки, но чат-боты и автоматические сервисы ответов сделали хороший шаг в этом направлении, заставив нас поверить, что мы действительно говорим с человеком, а не с роботом.

Наша цель в этой книге не пройти тест Тьюринга, но попробовать некоторые новые подходы к решению задач в машинном обучении, планировании, постановки целей, распознавании паттернов, группировке и кластеризации. Многие из этих задач окажутся очень сложными для решения каким-либо иным способом. Программа-ИИ, прошедшая тест Тьюринга будет считаться **сильным искусственным интеллектом**, или же цельным, работающим искусственным мозгом, и прямо как Вас, сильный ИИ не надо специально обучать для решения конкретной задачи. Сильный ИИ ещё не был создан, все что у нас есть сейчас - слабый ИИ, или программы, симулирующие мышление в какой-либо узкой области - распознавании объектов, выбирании хороших акций для покупки.

То, что мы будет создавать в этой книге не является сильным ИИ, и не надо волноваться, что наши создания разовьются и выйдут из под контроля. Это больше относится к научной фантастике и плохим фильмам, чем к тому, что мы имеем на сегодняшний день. Я уверен, что любой, кто проповедует о злом ИИ и предсказывает захват нашего мира роботами никогда не работал в этой сфере и не знает всего печального состояния исследований в области ИИ в части решения общих проблем или создания чего-либо, напоминающего разумность.
