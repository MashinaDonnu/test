function levenshteinDistance(s1, s2) {
    const len1 = s1.length;
    const len2 = s2.length;
    const matrix = [];

    for (let i = 0; i <= len1; i++) {
        matrix[i] = [i];
    }

    for (let j = 0; j <= len2; j++) {
        matrix[0][j] = j;
    }

    for (let i = 1; i <= len1; i++) {
        for (let j = 1; j <= len2; j++) {
            const cost = s1[i - 1] === s2[j - 1] ? 0 : 1;
            matrix[i][j] = Math.min(
                matrix[i - 1][j] + 1,
                matrix[i][j - 1] + 1,
                matrix[i - 1][j - 1] + cost
            );
        }
    }

    return matrix[len1][len2];
}

function findDifferences(urls1, urls2) {
    const differences = [];

    urls1.forEach(url1 => {
        let minDistance = Infinity;
        let closestUrl = '';

        urls2.forEach(url2 => {
            const distance = levenshteinDistance(url1, url2);
            if (distance < minDistance) {
                minDistance = distance;
                closestUrl = url2;
            }
        });

        if (minDistance !== 0) {
            differences.push({ url1, closestUrl });
        }
    });

    return differences;
}

// Пример использования
const urls1 = ['http://example.com', 'http://example.org', 'http://example.net'];
const urls2 = ['http://example.com', 'http://example.net', 'http://another-example.com'];

const differences = findDifferences(urls1, urls2);
console.log(differences);
