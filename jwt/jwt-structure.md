# JWT 구조

<details>
    <summary>header</summary>
    <ul>
        <li>header는 일반적으로 두 가지 요소를 가짐</li>
        <li>종류</li>
            <ul>
            <li>typ</li>
            <ul>
                <li>token의 type 지정</li>
                <li>즉 "JWT"</li>
            </ul>
            <li>alg</li>
            <ul>
                <li>hashing algorithm 지정</li>
                <li>보통 HMAC SHA256 또는 RSA 사용</li>
            </ul>
        <ul>
    </ul>
</details>
<details>
    <summary>payload</summary>
    <ul>
        <li>registered claim</li>
        <ul>
            <li>token에 대한 정보를 담기 위해 이름이 이미 정해진 claim</li>
            <li>registered claim의 사용은 optional</li>
            <li>종류</li>
            <ul>
                <li>iss: token 발급자(issuer)</li>
                <li>sub: token 제목(subject)</li>
                <li>aud: token 대상자(audience)</li>
                <li>exp: token 만료 시간(expiraton). 시간은 NumericDate 형식으로 되어 있어야 하며(ex: 1480849147370) 언제나 현재 시간보다 이후로 설정되어 있어야 함</li>
                <li>nbf: Not Before를 의미하며, token의 활성 날짜와 비슷한 개념. 여기에도 NumericDate 형식으로 날짜를 지정하며, 이 날짜가 지나기 전까지는 token이 처리되지 않음</li>
                <li>iat: token이 발급된 시간(issued at). 이 값을 사용하여 token의 age가 얼마나 되었는지 판단 가능</li>
                <li>jti: JWT의 고유 식별자. 주로 중복적인 처리를 방지하기 위하여 사용. 일회용 token에 사용하면 유용</li>
            </ul>
        </ul>
        <li>public clain</li>
        <ul>
            <li>충돌이 방지된(collision-resistant) 이름을 가지고 있어야 함</li>
            <li>위 조건을 만족하기 위해 claim 이름을 URI 형식으로 작명</li>
            <li>e.g. { "https://lemphis.com/jwt_claims/is_admin": true }</li>
        </ul>
        <li>private clain</li>
        <ul>
            <li>양 측간에(client <-> server) 협의하에 사용되는 claim</li>
            <li>registered claim의 사용은 optional</li>
            <li>충돌 가능성이 있으니 사용 시에 유의</li>
            <li>e.g. { "username": "lemphis" }</li>
        </ul>
    </ul>
</details>
<details>
    <summary>signature</summary>
    <ul>
        <li>header의 encoding값과 payload의 encoding값을 합친 후 주어진 secret key로 hash 생성</li>
        <li>base64 encoding이나 SHA256 등의 hashing은 보통 JWT library가 처리함</li>
    </ul>
</details>

> cf. https://jwt.io/introduction