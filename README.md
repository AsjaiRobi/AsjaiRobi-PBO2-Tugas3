# AsjaiRobi-PBO2-Tugas3
# Fitur Utama Program

    Masukkan Harga: User dapat memasukkan harga barang yang akan didiskon melalui textFieldHarga.
    Pilih Diskon: Program memiliki dua opsi untuk memilih diskon:
        ComboBox: Pilihan diskon berupa persentase dari 5% hingga 50%.
        Slider: Slider dapat disesuaikan dari 0% hingga 100%.
    Hitung Diskon: Tombol "Hitung" akan menghitung harga setelah diskon sesuai dengan harga yang dimasukkan dan nilai diskon yang dipilih.
    Reset: Tombol "Hapus" akan mereset semua input dan output.
    Keluar: Tombol "Keluar" untuk menutup program.

Penjelasan Kode

    Slider Diskon:

sliderDiskon.setMinimum(0);
sliderDiskon.setMaximum(100);
sliderDiskon.setMajorTickSpacing(10);
sliderDiskon.setMinorTickSpacing(5);
sliderDiskon.setPaintTicks(true);
sliderDiskon.setPaintLabels(true);

Kode di atas mengatur slider untuk nilai diskon dengan rentang 0 hingga 100, interval utama (major tick) setiap 10%, dan interval minor setiap 5%.

Pengaturan RadioButton untuk Mode Diskon:

radioSlider.addActionListener(e -> {
    comboDiskon.setEnabled(false);
    sliderDiskon.setEnabled(true);
});

radioComboBox.addActionListener(e -> {
    comboDiskon.setEnabled(true);
    sliderDiskon.setEnabled(false);
    radioSlider.setSelected(false);
});

Terdapat dua tombol radio (radioComboBox dan radioSlider) untuk memilih metode diskon. Jika radioSlider dipilih, ComboBox akan dinonaktifkan, dan slider diaktifkan. Sebaliknya, jika radioComboBox dipilih, slider akan dinonaktifkan dan ComboBox diaktifkan.

Menampilkan Nilai Diskon di Tooltip Slider:

sliderDiskon.addChangeListener(e -> {
    int nilaiDiskon = sliderDiskon.getValue();
    sliderDiskon.setToolTipText(nilaiDiskon + "%");
});

Ketika slider digeser, tooltip akan menunjukkan nilai persentase diskon yang dipilih.

Tombol Hitung:

private void jButton1ActionPerformed(java.awt.event.ActionEvent evt) {                                         
    try {
        double harga = Double.parseDouble(textFieldHarga.getText());
        double diskon;

        if (radioComboBox.isSelected()) {
            String selectedDiskon = (String) comboDiskon.getSelectedItem();
            diskon = Double.parseDouble(selectedDiskon.replace("%", "")) / 100;
        } else {
            diskon = sliderDiskon.getValue() / 100.0;
        }

        double hargaDiskon = harga - (harga * diskon);
        textAreaOutput.setText("Harga setelah diskon: Rp" + hargaDiskon);
    } catch (NumberFormatException ex) {
        JOptionPane.showMessageDialog(null, "Masukkan harga yang valid.");
    }
}

Saat tombol "Hitung" diklik, program akan mengambil harga dari textFieldHarga dan mengonversinya menjadi angka. Program kemudian menghitung diskon berdasarkan opsi yang dipilih (ComboBox atau Slider) dan menampilkan harga setelah diskon di textAreaOutput.

Tombol Hapus:

private void jButton2ActionPerformed(java.awt.event.ActionEvent evt) {                                         
    textFieldHarga.setText("");
    textAreaOutput.setText("");
    sliderDiskon.setValue(0);
    comboDiskon.setSelectedIndex(0);
}

Tombol ini akan mereset semua input dan output, mengosongkan textFieldHarga, textAreaOutput, mengatur slider ke 0%, dan mengembalikan ComboBox ke pilihan pertama.

Tombol Keluar:

private void jButton3ActionPerformed(java.awt.event.ActionEvent evt) {                                         
    System.exit(0);
}

Tombol "Keluar" akan menutup aplikasi.
