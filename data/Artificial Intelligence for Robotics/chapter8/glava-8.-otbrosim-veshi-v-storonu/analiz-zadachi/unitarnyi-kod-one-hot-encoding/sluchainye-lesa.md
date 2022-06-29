# 8.3.3.1.Случайные леса

Я действительно хотел добавить этот раздел о случайных лесных классификаторах, просто потому, что название звучит чертовски круто. Были даже разговоры об экстремальных случайных лесах. Хотя я могу быть обвинен в растяжении метафор до предела, на этот раз имя вдохновлено программным обеспечением. Мы узнали, как создавать деревья решений, и мы узнали, что у них есть слабые места. Лучше всего, если данные действительно принадлежат дифференцированным группам. Но это не очень терпимо к «шуму» в данных. И дерево действительно становится громоздким, если вы хотите увеличить его - вы можете себе представить, насколько большой график получится с 200 классами, а не с шестью или с семью, с которыми мы имели дело.

Если вы хотите воспользоваться простотой и полезностью деревьев решений, но хотели бы обрабатывать больше данных, больше неопределенностей и больше классов, вы можете использовать случайный лес, который, как видно из названия - просто целая партия случайно сгенерированных деревьев решений. Давайте пройдемся по процессу.

Мы собираем нашу базу данных информации, но вместо 18 строк в нашей базе данных мы имеем 10000 записей или 1 миллион записей. Мы подразделяем эти данные на случайные множества – генерируем 100 наборов данных, каждый из которых случайным образом выбирается из всех наших данных, и мы помещаем их в случайном порядке. Мы также извлекаем один набор данных для использования в качестве тестового набора, как мы это делали для нейронных сетей.

Теперь для каждого набора случайных данных мы создаем дерево решений, используя тот же процесс, который мы уже изучили.

Теперь у нас есть коллекция из 100 классификационных двигателей, каждый из которых создан по-разному, случайно сгенерированное подмножество данных. Теперь мы проверим наш случайный лес, взяв данные из тестового набора и пробежимся через все 100 деревьев в нашем лесу. Каждое дерево обеспечит оценку классификации данных в нашей записи испытаний. Если мы все еще классифицируем игрушки, тогда одно из деревьев оценило бы, что мы описываем игрушечную машинку. Другое может подумать, что это музыкальный инструмент. Мы берем каждую оценку и рассматриваем ее как голосование. Дальше главное правило - класс, который выбрали большинство деревьев является победителем. На этом все.

Настройка и программа точно такие же, как и раньше, но вы не можете нарисовать дерево решений из случайного леса, или просто создать дерево как самоцель, потому что это не то, что делает случайный лес - если вам просто нужно дерево решений, вы знаете, как это сделать. Что вы можете сделать, это использовать случайный лес, как нейронную сеть, в качестве классификации двигателя \(к какому классу принадлежат эти данные?\) или двигателя регрессии, которая приближается к нелинейной кривой.
