# walkie-talkie
Делаем рацию на 433,92 МГц (LPD диапазон)

# Задача
Необходимо реализовать следующий функционал:
1. Разделение каналов по частотам
2. Разделение каналов по группам
3. Пороговое устройство (и на передачу и на прием)

# Реализация
```mermaid
flowchart TB
  antenna["Антенна"]
  switch["Переключатель"]
  voltahe_source["DC-DC 5V"]
  arduino["Arduino"]
  transmitter["Передатчик"]
  receiver["Приемник"]
  amplifier["Усилитель"]
  micro["Микрофон"]
  speaker["Динамик"]
  mixer_up["Повышающий смеситель"]
  mixer_down["Понижающий смеситель"]
  threshold_rx["Пороговое устройство"]
  threshold_tx["Пороговое устройство"]

  subgraph Приемник
    receiver
    mixer_down
    threshold_rx
  end

  subgraph Передатчик
    transmitter
    mixer_up
    threshold_tx
  end

  micro --> amplifier
  amplifier --> threshold_tx
  amplifier --> mixer_up
  mixer_up --> transmitter
  threshold_tx --> arduino
  arduino --> transmitter
  transmitter --> switch
  switch --> antenna

  antenna --> switch
  switch --> receiver
  receiver --> mixer_down
  mixer_down --> threshold_rx
  threshold_rx --> arduino
  arduino --> speaker
  threshold_rx --> speaker
  
  
  
  
  

```

# Компоненты
- Питание от 9В кроны через [DC-DC преобразователь](https://amperkot.ru/products/dcdc_preobrazovatel_ponizhayuschiy_lm2596s/24022294.html) на 5 вольт.  
- Передача и прием осуществляются переделанными [радиомодулями](https://amperkot.ru/products/radiomoduli_433mhz_peredatchik_mxfs03v_i_priemnik_mx05v/23869814.html) ([Видео](https://www.youtube.com/watch?v=o1lduXJH_W4&ab_channel=ZAFERYILDIZ)).  
- Логика реализована на [ардуинке](https://amperkot.ru/products/plata_nano_v_30__arduinosovmestimaya/23813247.html).  
- [Микрофон](https://amperkot.ru/products/elektretnyiy_mikrofon_6x5mm_emb6050ul_52d/24145498.html)
- [Усилитель микрофона](Усилитель%20микрофона.md)
