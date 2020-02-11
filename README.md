### Описание

Пакет, реализующий алгоритм трансформации "urn://smev-gov-ru/xmldsig/transform"

### Зачем

При подписании XML-фрагментов ЭП в формате XMLDSig, обязательно использование трансформации urn://smev-gov-ru/xmldsig/transform.

### Алгорим трансформации

1. XML declaration и processing instructions, если есть, вырезаются;
2. Если текстовый узел содержит только пробельные символы (код символа меньше или равен '\u0020'), этот текстовый узел вырезается;
3. После применения правил из пунктов 1 и 2, если даже у элемента нет дочерних узлов, элемент не может быть представлен в виде empty element tag (http://www.w3.org/TR/2008/REC-xml-20081126/#sec-starttags, правило [44]), а должен быть преобразован в пару start-tag + end-tag;
4. Удалить namespace prefix, которые на текущем уровне объявляются, но не используются;
5. Проверить, что namespace текущего элемента объявлен либо выше по дереву, либо в текущем элементе. Если не объявлен, объявить в текущем элементе;
6. Namespace prefix элементов и атрибутов должны быть заменены на автоматически сгенерированные. Сгенерированный префикс состоит из литерала «ns», и порядкового номера сгенерированного префикса в рамках обрабатываемого XML-фрагмента, начиная с единицы. При генерации префиксов должно устраняться их дублирование; 
7. Атрибуты должны быть отсортированы в алфавитном порядке: сначала по namespace URI (если атрибут - в qualified form), затем – по local name. Атрибуты в unqualified form после сортировки идут после атрибутов в qualified form;
8. Объявления namespace prefix должны находиться перед атрибутами. Объявления префиксов должны быть отсортированы в порядке объявления, а именно:
    + Первым объявляется префикс пространства имён элемента, если он не был объявлен выше по дереву;
    + Дальше объявляются префиксы пространств имён атрибутов, если они требуются. Порядок этих объявлений соответствует порядку атрибутов, отсортированных в алфавитном порядке (см. п.7 текущего перечня).

### Использование
```php
use Danbka\Smev\Transform;

$transform = new Transform();
$transform->process($xml);
```