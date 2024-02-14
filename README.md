function deepCompare(obj1, obj2, path = '') {
    // Проверяем типы объектов
    if (typeof obj1 !== 'object' || typeof obj2 !== 'object' || obj1 === null || obj2 === null) {
        if (obj1 !== obj2) {
            console.log(`Difference at ${path}: ${obj1} !== ${obj2}`);
        }
        return obj1 === obj2;
    }

    const keys1 = Object.keys(obj1);
    const keys2 = Object.keys(obj2);

    // Проверяем количество ключей
    if (keys1.length !== keys2.length) {
        console.log(`Difference at ${path}: Different number of keys`);
        return false;
    }

    let isEqual = true;

    // Проверяем каждый ключ и его соответствующее значение рекурсивно
    for (const key of keys1) {
        const currentPath = (path ? path + '.' : '') + key;
        if (!keys2.includes(key)) {
            console.log(`Difference at ${currentPath}: Key does not exist in second object`);
            isEqual = false;
        } else {
            isEqual = deepCompare(obj1[key], obj2[key], currentPath) && isEqual;
        }
    }

    return isEqual;
}

// Пример использования
const obj1 = { a: 1, b: { c: 2, d: [3, 4] } };
const obj2 = { a: 1, b: { c: 3, e: [3, 4] } };
deepCompare(obj1, obj2);
