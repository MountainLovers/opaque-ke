## 本地保存的结构体
### Client
ClientRegistration:
    alpha: 实际上就是M，即 P * r
    token: oprf::Token类型
        data: 用户的password
        blind: 标量r

### Server
ServerSetup:  通过ServerSetup::new()新建
    oprf_seed: the server-side seed of Nh bytes used to generate an oprf_key.
    keypair:
    fake_keypair:
    

## 传输的结构体(messages.rs)
RegistrationRequest:    Client --> Server
    alpha:  同上

RegistrationResponse:   Server --> Client
    beta:   
    server_s_pk:

## 函数过程解析
ClientRegistration::start
    - input: 
      - blinding_factor_rng
      - password
    - output:
      - ClientRegistrationStartResult
        - message: RegistrationRequest
        - state: ClientRegistration

ServerRegistration::start
    - input: 411
      - server_setup: <ServerSetup>
      - message: <RegistrationRequest>
      - credential_identifier: an identifier that uniquely represents the credential being
  registered.

ClientRegistration::finish

## 局部函数解析
Blind(x): 
    1. 把x转化为oprf Group中的点p
    2. 随机选择标量r
    3. 计算M=p^r
    4. 返回(r, M)

